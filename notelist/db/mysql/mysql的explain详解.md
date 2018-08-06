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
rows          | 本次查询预计扫描的记录数,是一个预估值,不是精准值
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
```sql
explain select * from t_student

-- 运行结果
+----+-------------+-----------+------------+------+---------------+--------+---------+--------+------+----------+--------+
| id | select_type | table     | partitions | type | possible_keys | key    | key_len | ref    | rows | filtered | Extra  |
+----+-------------+-----------+------------+------+---------------+--------+---------+--------+------+----------+--------+
| 1  | SIMPLE      | t_student | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4    | 100.0    | <null> |
+----+-------------+-----------+------------+------+---------------+--------+---------+--------+------+----------+--------+
```

#### select_type primary
```sql
explain 
	select * 
	from t_student 
union 
	select * 
	from t_student t1 
union 
	select * 
	from t_student t2

-- 运行结果
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| id     | select_type  | table        | partitions | type | possible_keys | key    | key_len | ref    | rows   | filtered | Extra           |
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| 1      | PRIMARY      | t_student    | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 2      | UNION        | t1           | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 3      | UNION        | t2           | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| <null> | UNION RESULT | <union1,2,3> | <null>     | ALL  | <null>        | <null> | <null>  | <null> | <null> | <null>   | Using temporary |
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+  
```

#### select_type union
```sql
explain 
	select * 
	from t_student 
union 
	select * 
	from t_student t1 
union 
	select * 
	from t_student t2

-- 运行结果
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| id     | select_type  | table        | partitions | type | possible_keys | key    | key_len | ref    | rows   | filtered | Extra           |
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| 1      | PRIMARY      | t_student    | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 2      | UNION        | t1           | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 3      | UNION        | t2           | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| <null> | UNION RESULT | <union1,2,3> | <null>     | ALL  | <null>        | <null> | <null>  | <null> | <null> | <null>   | Using temporary |
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+  

```

#### select_type dependent union

#### select_type union result
- union result表示union查询的结果
- 示例
```sql
explain 
	select * 
	from t_student 
union 
	select * 
	from t_student t1 
union 
	select * 
	from t_student t2

-- 运行结果
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| id     | select_type  | table        | partitions | type | possible_keys | key    | key_len | ref    | rows   | filtered | Extra           |
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| 1      | PRIMARY      | t_student    | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 2      | UNION        | t1           | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 3      | UNION        | t2           | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| <null> | UNION RESULT | <union1,2,3> | <null>     | ALL  | <null>        | <null> | <null>  | <null> | <null> | <null>   | Using temporary |
+--------+--------------+--------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+  

```


#### select_type subquery
```sql
explain 
	select * 
	from t_student 
	where 
	  sid =(
	    select sid 
	    from t_student_course 
	    where id = 1
	  )

-- 运行结果
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+--------------------------------+
| id | select_type | table  | partitions | type   | possible_keys | key    | key_len | ref    | rows   | filtered | Extra                          |
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+--------------------------------+
| 1  | PRIMARY     | <null> | <null>     | <null> | <null>        | <null> | <null>  | <null> | <null> | <null>   | no matching row in const table |
| 2  | SUBQUERY    | <null> | <null>     | <null> | <null>        | <null> | <null>  | <null> | <null> | <null>   | no matching row in const table |
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+--------------------------------+  
```

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
	select * 
	from t_student 
union 
	select * 
	from t_student t1

--运行结果
+--------+--------------+------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| id     | select_type  | table      | partitions | type | possible_keys | key    | key_len | ref    | rows   | filtered | Extra           |
+--------+--------------+------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
| 1      | PRIMARY      | t_student  | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| 2      | UNION        | t1         | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 4      | 100.0    | <null>          |
| <null> | UNION RESULT | <union1,2> | <null>     | ALL  | <null>        | <null> | <null>  | <null> | <null> | <null>   | Using temporary |
+--------+--------------+------------+------------+------+---------------+--------+---------+--------+--------+----------+-----------------+
```

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
- 示例
```sql

-- 根据主键查询
explain select * from t_student where sid=1;

-- 根据主键查询查询结果如下
+----+-------------+-----------+------------+-------+---------------+---------+---------+-------+------+----------+--------+
| id | select_type | table     | partitions | type  | possible_keys | key     | key_len | ref   | rows | filtered | Extra  |
+----+-------------+-----------+------------+-------+---------------+---------+---------+-------+------+----------+--------+
| 1  | SIMPLE      | t_student | <null>     | const | PRIMARY       | PRIMARY | 4       | const | 1    | 100.0    | <null> |
+----+-------------+-----------+------------+-------+---------------+---------+---------+-------+------+----------+--------+

-- 根据唯一索引查询
explain select * from t_student where mobile='18612211111';	

-- 根据唯一索引查询查询结果如下
+----+-------------+-----------+------------+-------+----------------+----------------+---------+-------+------+----------+--------+
| id | select_type | table     | partitions | type  | possible_keys  | key            | key_len | ref   | rows | filtered | Extra  |
+----+-------------+-----------+------------+-------+----------------+----------------+---------+-------+------+----------+--------+
| 1  | SIMPLE      | t_student | <null>     | const | uni_inx_mobile | uni_inx_mobile | 36      | const | 1    | 100.0    | <null> |
+----+-------------+-----------+------------+-------+----------------+----------------+---------+-------+------+----------+--------+

```

#### type eq_ref
- 表连接时基于主键或非NULL的唯一索引完成扫描
- 示例

#### type ref
- 基于索引的等值查询，或者表间等值连接
- 示例
```sql
-- 根据普通索引查询
explain select * from t_student where student_age=20;

-- 根据普通索引查询结果
+----+-------------+-----------+------------+------+-----------------+-----------------+---------+-------+------+----------+--------+
| id | select_type | table     | partitions | type | possible_keys   | key             | key_len | ref   | rows | filtered | Extra  |
+----+-------------+-----------+------------+------+-----------------+-----------------+---------+-------+------+----------+--------+
| 1  | SIMPLE      | t_student | <null>     | ref  | inx_student_age | inx_student_age | 4       | const | 1    | 100.0    | <null> |
+----+-------------+-----------+------------+------+-----------------+-----------------+---------+-------+------+----------+--------+



```

#### type fulltext

#### type ref_or_null

#### type unique_subquery

#### type index_subquery

#### type range
- 利用索引进行范围查询
- 示例
```sql
-- 根据索引进行 between and查询
explain select * from t_student where student_age between 1 and 20;

-- 根据索引进行 between and查询结果
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+--------+------+----------+-----------------------+
| id | select_type | table     | partitions | type  | possible_keys   | key             | key_len | ref    | rows | filtered | Extra                 |
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+--------+------+----------+-----------------------+
| 1  | SIMPLE      | t_student | <null>     | range | inx_student_age | inx_student_age | 4       | <null> | 2    | 100.0    | Using index condition |
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+--------+------+----------+-----------------------+


-- 根据索引进行>查询
explain select * from t_student where student_age>20;

-- 根据索引进行>查询结果
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+--------+------+----------+-----------------------+
| id | select_type | table     | partitions | type  | possible_keys   | key             | key_len | ref    | rows | filtered | Extra                 |
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+--------+------+----------+-----------------------+
| 1  | SIMPLE      | t_student | <null>     | range | inx_student_age | inx_student_age | 4       | <null> | 2    | 100.0    | Using index condition |
+----+-------------+-----------+------------+-------+-----------------+-----------------+---------+--------+------+----------+-----------------------+


```
#### type index



### possible_keys
- 可能选择的索引


### key
- 本次查询实际使用的索引


### key_len
- 本次查询用于结果过滤的索引实际长度(字节数) 

### ref

### rows
- 本次查询预计扫描的记录数,是一个预估值,不是精准值

### filtered

### Extra
值     | 含义
----------| -------------
Using index    | 
Using filesort  | 将用外部排序而不是按照索引顺序排列结果，数据较少时从内存排序，否则需要在磁盘完成排序，代价非常高，需要添加合适的索引
Using temporary  | 需要创建一个临时表来存储结果，这通常发生在对没有索引的列进行GROUP BY时，或者ORDER BY里的列不都在索引里，需要添加合适的索引
Using where      |
Impossible WHERE | 对Where子句判断的结果总是false而不能选择任何数据

#### Impossible WHERE
```sql
explain select * from t_student where 1=0;

-- 运行结果
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+------------------+
| id | select_type | table  | partitions | type   | possible_keys | key    | key_len | ref    | rows   | filtered | Extra            |
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+------------------+
| 1  | SIMPLE      | <null> | <null>     | <null> | <null>        | <null> | <null>  | <null> | <null> | <null>   | Impossible WHERE |
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+------------------+
```


#### Extra No tables used
```sql
explain select 1;

-- 运行结果
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+----------------+
| id | select_type | table  | partitions | type   | possible_keys | key    | key_len | ref    | rows   | filtered | Extra          |
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+----------------+
| 1  | SIMPLE      | <null> | <null>     | <null> | <null>        | <null> | <null>  | <null> | <null> | <null>   | No tables used |
+----+-------------+--------+------------+--------+---------------+--------+---------+--------+--------+----------+----------------+

```

#### Extra Using index 
- The column information is retrieved from the table using only information in the index tree without having to do an additional seek to read the actual row. This strategy can be used when the query uses only columns that are part of a single index
```sql
-- 
explain select  sid, student_age from t_student where student_age=30;

-- 运行结果
+----+-------------+-----------+------------+------+-----------------+-----------------+---------+-------+------+----------+-------------+
| id | select_type | table     | partitions | type | possible_keys   | key             | key_len | ref   | rows | filtered | Extra       |
+----+-------------+-----------+------------+------+-----------------+-----------------+---------+-------+------+----------+-------------+
| 1  | SIMPLE      | t_student | <null>     | ref  | inx_student_age | inx_student_age | 4       | const | 2    | 100.0    | Using index |
+----+-------------+-----------+------------+------+-----------------+-----------------+---------+-------+------+----------+-------------+
```


#### Extra Using filesort
- 将用外部排序而不是按照索引顺序排列结果，数据较少时从内存排序，否则需要在磁盘完成排序，代价非常高，需要添加合适的索引
```sql
--  在order by的字段上没有索引
explain select sid from t_student_course order by cid;

--  在order by的字段上没有索引运行结果
+----+-------------+------------------+------------+------+---------------+--------+---------+--------+------+----------+----------------+
| id | select_type | table            | partitions | type | possible_keys | key    | key_len | ref    | rows | filtered | Extra          |
+----+-------------+------------------+------------+------+---------------+--------+---------+--------+------+----------+----------------+
| 1  | SIMPLE      | t_student_course | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 1    | 100.0    | Using filesort |
+----+-------------+------------------+------------+------+---------------+--------+---------+--------+------+----------+----------------+

```

#### Extra Using temporary
- 需要创建一个临时表来存储结果，这通常发生在对没有索引的列进行GROUP BY时，或者ORDER BY里的列不都在索引里，需要添加合适的索引

```sql
-- 在group by上的字段没有加索引
explain select cid  from t_student_course group by cid;

-- 在group by上的字段没有加索引运行结果
+----+-------------+------------------+------------+------+---------------+--------+---------+--------+------+----------+---------------------------------+
| id | select_type | table            | partitions | type | possible_keys | key    | key_len | ref    | rows | filtered | Extra                           |
+----+-------------+------------------+------------+------+---------------+--------+---------+--------+------+----------+---------------------------------+
| 1  | SIMPLE      | t_student_course | <null>     | ALL  | <null>        | <null> | <null>  | <null> | 1    | 100.0    | Using temporary; Using filesort |
+----+-------------+------------------+------------+------+---------------+--------+---------+--------+------+----------+---------------------------------+
```

### 参考文章
https://dev.mysql.com/doc/refman/5.7/en/explain-output.html
http://imysql.com/2015/11/04/mysql-faq-some-important-in-explain.shtml
http://imysql.com/2015/10/20/mysql-faq-key-len-in-explain.shtml



