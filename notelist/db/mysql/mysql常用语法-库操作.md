## mysql常用语法-库操作

#### 创建db
- 语法格式
```mysql
CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name
    [create_specification] ...

create_specification:
    [DEFAULT] CHARACTER SET [=] charset_name
  | [DEFAULT] COLLATE [=] collation_name
``` 

- 样例
```mysql
create database test01 default character set utf8 default collate utf8_general_ci;
```


#### 查询db列表
```mysql
show databases;
```
#### 切换到指定的db
```mysql
use test01;
```
#### 删除指定的db
```mysql
drop database test01;
```

#### 查看某个库里有哪些表
```mysql
show tables;
```