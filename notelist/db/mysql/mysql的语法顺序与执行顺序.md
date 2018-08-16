## mysql的语法顺序与执行顺序
> sql语句的执行顺序跟其语句的语法顺序并不一致

#### sql语法顺序如下:
- select[distinct]
- from
- where
- group by
- having
- union
- order by

#### sql执行顺序如下:
- from
- where
- group by
- having
- select
- distinct
- union
- order by


