## mysql show syntax


```sql
show {binary | master} logs
show binlog events [in 'log_name'] [from pos] [limit [offset,] row_count]
show character set [like_or_where]
show collation [like_or_where]
show [full] columns from tbl_name [from db_name] [like_or_where]
show create database db_name
show create event event_name
show create function func_name
show create procedure proc_name
show create table tbl_name
show create trigger trigger_name
show create view view_name
show databases [like_or_where]
show engine engine_name {status | mutex}
show [storage] engines
show errors [limit [offset,] row_count]
show events
show function code func_name
show function status [like_or_where]
show grants for user
show index from tbl_name [from db_name]
show master status
show open tables [from db_name] [like_or_where]
show plugins
show procedure code proc_name
show procedure status [like_or_where]
show privileges
show [full] processlist
show profile [types] [for query n] [offset n] [limit n]
show profiles
show relaylog events [in 'log_name'] [from pos] [limit [offset,] row_count]
show slave hosts
show slave status [for channel channel]
show [global | session] status [like_or_where]
show table status [from db_name] [like_or_where]
show [full] tables [from db_name] [like_or_where]
show triggers [from db_name] [like_or_where]
show [global | session] variables [like_or_where]
show warnings [limit [offset,] row_count]

like_or_where:
    like 'pattern'
  | where expr
```


链接(https://dev.mysql.com/doc/refman/5.7/en/show.html)



