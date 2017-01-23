## mysql的my.cnf文件加载顺序查询
```shell
$ which mysqld
/usr/local/mysql/bin/mysqld

$ /usr/local/mysql/bin/mysqld --verbose --help|grep -A 1 'Default options'
Default options are read from the following files in the given order:
/etc/my.cnf /etc/mysql/my.cnf /usr/local/mysql/etc/my.cnf ~/.my.cnf
```

