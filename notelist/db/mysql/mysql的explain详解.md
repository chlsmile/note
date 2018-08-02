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
type          | 连接类型
possible_keys | 可能选择的索引
key           | 实际使用的索引
key_len       | 查询使用的索引的字节数
ref           | //TODO
rows          | 查询需要扫描的行数, 在innodb引擎的表里这个值是一个预估值，可能不是精准的
filtered      | //TODO
Extra         | 一些额外信息


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
- 连接类型，比较重要的性能指标，性能从好到差顺序依次为system`>`const->eq_ref->ref->fulltext->ref_or_null->ref_or_null->unique_subquery->index_subquery->range->index->ALL

### possible_keys

### key

### key_len

### ref

### rows

### filtered

### Extra


