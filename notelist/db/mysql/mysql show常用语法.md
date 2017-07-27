## mysql show 常用语法
#### 1.show binary logs syntax
```sql
show binary logs
show master logs
```

Lists the binary log files on the server

```sql
 mysql> show binary logs;
 +---------------+-----------+
 | Log_name      | File_size |
 +---------------+-----------+
 | binlog.000015 |    724935 |
 | binlog.000016 |    733481 |
 +---------------+-----------+
```

show master logs is equivalent to show binary logs.

#### 2. show binlog events syntax

```sql
SHOW BINLOG EVENTS
   [IN 'log_name']
   [FROM pos]
   [LIMIT [offset,] row_count]
```

Shows the events in the binary log. If you do not specify 'log_name', the first binary log is displayed.



#### 3. show character set syntax
```sql
SHOW CHARACTER SET
    [LIKE 'pattern' | WHERE expr]
```



https://dev.mysql.com/doc/refman/5.7/en/show.html



