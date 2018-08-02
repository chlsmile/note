## explain详解

#### explain 输出列详解
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


#### 测试数据
- 建一些测试表与数据(https://github.com/datacharmer/test_db), 选择employees.sql导入


#### id

#### select_type

#### table

#### partitions

#### type

#### possible_keys

#### key

#### key_len

#### ref

#### rows

#### filtered

#### Extra


