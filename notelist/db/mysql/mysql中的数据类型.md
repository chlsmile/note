## mysql中的数据类型
### mysql版本
- 5.7.19-log MySQL Community Server (GPL)



### 整数类型
类型      | 存储空间(字节数) |有符号最小值|无符号最小值|有符号最大值|无符号最大值
----------| -------------|-------------|-------------|-------------|-------------|
tinyint   |1|-128		|0|127			|255|
smallint  |2|-32768		|0|32767		|65535|
mediumint |3|-8388608	|0|8388607		|16777215|
int       |4|-2147483648|0|2147483647	|4294967295
bigint    |8|-2^65535 	|0|2^63-1		|2^64-1

### DECIMAL, NUMERIC类型

### bit类型

### 浮点数类型FLOAT, DOUBLE


### 日期与时间
类型      |支持范围
----------|----------
date|  '1000-01-01' to '9999-12-31'
datetime|'1000-01-01 00:00:00' to '9999-12-31 23:59:59'
timestamp|'1970-01-01 00:00:01' UTC to '2038-01-19 03:14:07' UTC
time|
year|

### 字符串类型
类型|范围|
char|0~255|
varchar|0~65535|
binary|
varbinary|
tinyblob|
blob|
mediumblob|
longblob|
tinytext|
text|
mediumtext|
longtext|
enum|
set|

- char类型的特点是长度固定,长度为创建表时声明的长度,如果实际存储的字符数小于定义的长度,在存储的时候会在后面添加相应位数的空格进行填充,在获取数据的时候会去掉尾部的空格(如果使用sql_mode = 'PAD_CHAR_TO_FULL_LENGTH'则会有变化,具体参考mysql文档)
- varchar类型的特点是长度可变,VARCHAR值存储为1字节或2字节的长度的前缀加数据
