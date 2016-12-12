## mysql常用语法-表操作

- 创建表
```mysql
create table t_student (
  id bigint(20) unsigned not null  auto_increment comment '主键,自增长',
  name varchar(50) not null default '' comment '姓名',
  mobile varchar(20) not null default '' comment '电话',
  age tinyint(3) not null comment '年龄',
  home_addr varchar(200) not null default '' comment '住址',
  remark varchar(100) default NULL comment '备注',
  create_time datetime not null comment '创建时间',
  update_time datetime not null comment '更新时间',
  primary key(id)
) engine=InnoDB default charset=utf8 comment='学生表';
```
- 删除表
```mysql
drop table t_student;
```

- 修改表-增加字段
```mysql
alter table t_student add column school varchar(100) default NULL comment '学校';
```
- 修改表-删除字段
```mysql
alter table t_student drop column school;
```
- 修改表-增加索引
```mysql

```

- 修改表-删除索引
```mysql

```