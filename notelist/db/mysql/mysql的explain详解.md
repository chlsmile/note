## explain详解 //TODO 还没整理完
### mysql版本
- 5.7.19-log MySQL Community Server (GPL)

### explain 输出列详解
列      | 含义
----------| -------------
id            | 查询标识
select_type   | 查询类型
table         | 表名
partitions    | 分区
type          | 本次查询表联接类型，从这里可以看到本次查询大致的效率
possible_keys | 可能选择的索引
key           | 本次查询实际使用的索引
key_len       | 本次查询用于结果过滤的索引实际长度(字节数)
ref           | //TODO
rows          | 本次查询预计扫码的记录数, 在innodb引擎的表里这个值是一个预估值，可能不是精准的
filtered      | //TODO
Extra         | 额外附加信息


### 测试数据
- 建一些测试表与数据(https://github.com/datacharmer/test_db), 选择employees.sql导入


### id

### select_type
查询类型     | 含义
----------| -------------
simple |  简单的查询不包含union查询和子查询
primary|  最外层的查询
union | 
dependent union| 
union result| 
subquery| 
dependent subquery| 
derived|
materialized|
uncacheable subquery|
uncacheable union| 

#### select_type simple

#### select_type primary

#### select_type union


#### select_type dependent union

#### select_type union result
- union result表示union查询的结果
- 示例
```sql
explain 
	select * from employees
union 
	select * from employees 
union 
	select * from employees;
```
- 运行结果
mysql-explain-select-type-union-result.png


#### select_type subquery

#### select_type dependent subquery

#### select_type derived 
- derived 表示派生表

#### select_type materialized 

#### select_type uncacheable subquery

#### select_type uncacheable union


### table

- 示例
```sql
explain 
    select * from employees 
 union 
    select * from employees t2
```
- 运行结果
mysql-explain-table.png

### partitions

### type
- 本次查询表联接类型，从这里可以看到本次查询大致的效率，比较重要的性能指标
- 性能从好到差顺序依次为`system`>`const`>`eq_ref`>`ref`>`fulltext`>`ref_or_null`>`index_merge`>`unique_subquery`>`index_subquery`>`range`>`index`>`ALL`
- type类型与含义

类型     | 含义
----------| -------------
system |  查询对象表只有一行数据，这是最好的情况
const | 基于主键或唯一索引唯一值查询，最多返回一条结果
eq_ref | 表连接时基于主键或非NULL的唯一索引完成扫描
ref | 	基于索引的等值查询，或者表间等值连接
fulltext | 全文检索
ref_or_null | 表连接类型是ref，但进行扫描的索引列中可能包含NULL值
index_merge | 可以利用index merge特性用到多个索引，提高查询效率
unique_subquery | 子查询中可以用到唯一索引
index_subquery | 子查询中可以用到索引
range | 利用索引进行范围查询
index | 执行full index scan，并且可以通过索引完成结果扫描并且直接从索引中取的想要的结果数据，也就是可以避免回表
ALL | 全表扫描	

#### type system
- The table has only one row (= system table). This is a special case of the const join type.
- 表中只有一条记录(系统表),是一种特殊的const类型
- 举例
```sql
//TODO 目前还没有找到合适的例子
```

#### type const
- 基于主键或唯一索引唯一值查询，最多返回一条结果
- 举例
```sql
-- 根据主键查询
explain select * from t_student where id=1;

-- 根据主键查询查询结果如下
+----+-------------+-----------+------------+-------+---------------+---------+---------+-------+------+----------+--------+
| id | select_type | table     | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra  |
+----+-------------+-----------+------------+-------+---------------+---------+---------+-------+------+----------+--------+
| 1  | SIMPLE      | t_student | <null>     | const | PRIMARY       | PRIMARY | 4       | const | 1    | 100.0    | <null> |
+----+-------------+-----------+------------+-------+---------------+---------+---------+-------+------+----------+--------+

-- 根据唯一索引查询
explain select * from t_student where student_no=1102;

-- 根据唯一索引查询查询结果如下
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+-------+------+----------+--------+
| id | select_type | table     | partitions | type  | possible_keys   | key             | key_len | ref   | rows | filtered | Extra  |
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+-------+------+----------+--------+
| 1  | SIMPLE      | t_student | <null>     | const | uinx_student_no | uinx_student_no | 4       | const | 1    | 100.0    | <null> |
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+-------+------+----------+--------+

```

#### type eq_ref

#### type ref

#### type fulltext

#### type ref_or_null

#### type unique_subquery

#### type index_subquery

#### type range

#### type index

#### type index

### possible_keys

### key

### key_len

### ref

### rows

### filtered

### Extra

### 参考文章
https://dev.mysql.com/doc/refman/5.7/en/explain-output.html
http://imysql.com/2015/11/04/mysql-faq-some-important-in-explain.shtml
http://imysql.com/2015/10/20/mysql-faq-key-len-in-explain.shtml



