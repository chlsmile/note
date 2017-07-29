## mysql查询常用变量信息

#### 查询dir
```sql
show variables like '%dir%';
```

```sql
mysql> show variables like '%dir%';
+-----------------------------------------+---------------------------------------------------+
| Variable_name                           | Value                                             |
+-----------------------------------------+---------------------------------------------------+
| basedir                                 | /usr/local/mysql/                                 |
| binlog_direct_non_transactional_updates | OFF                                               |
| character_sets_dir                      | /usr/local/mysql/share/charsets/                  |
| datadir                                 | /usr/local/mysql/data/                            |
| ignore_db_dirs                          |                                                   |
| innodb_data_home_dir                    |                                                   |
| innodb_log_group_home_dir               | ./                                                |
| innodb_max_dirty_pages_pct              | 75.000000                                         |
| innodb_max_dirty_pages_pct_lwm          | 0.000000                                          |
| innodb_tmpdir                           |                                                   |
| innodb_undo_directory                   | ./                                                |
| lc_messages_dir                         | /usr/local/mysql/share/                           |
| plugin_dir                              | /usr/local/mysql/lib/plugin/                      |
| slave_load_tmpdir                       | /var/folders/6f/dfj0n7k16v7cngl7v86rthr80000gn/T/ |
| tmpdir                                  | /var/folders/6f/dfj0n7k16v7cngl7v86rthr80000gn/T/ |
+-----------------------------------------+---------------------------------------------------+
```

#### 查询log
```sql
mysql> show variables like '%log%';
```
```sql
+-----------------------------------------+---------------------------------------------+
| Variable_name                           | Value                                       |
+-----------------------------------------+---------------------------------------------+
| back_log                                | 80                                          |
| binlog_cache_size                       | 32768                                       |
| binlog_checksum                         | CRC32                                       |
| binlog_direct_non_transactional_updates | OFF                                         |
| binlog_error_action                     | ABORT_SERVER                                |
| binlog_format                           | ROW                                         |
| binlog_group_commit_sync_delay          | 0                                           |
| binlog_group_commit_sync_no_delay_count | 0                                           |
| binlog_gtid_simple_recovery             | ON                                          |
| binlog_max_flush_queue_time             | 0                                           |
| binlog_order_commits                    | ON                                          |
| binlog_row_image                        | FULL                                        |
| binlog_rows_query_log_events            | OFF                                         |
| binlog_stmt_cache_size                  | 32768                                       |
| expire_logs_days                        | 0                                           |
| general_log                             | OFF                                         |
| general_log_file                        | /usr/local/mysql/data/bogon.log             |
| innodb_api_enable_binlog                | OFF                                         |
| innodb_flush_log_at_timeout             | 1                                           |
| innodb_flush_log_at_trx_commit          | 1                                           |
| innodb_locks_unsafe_for_binlog          | OFF                                         |
| innodb_log_buffer_size                  | 16777216                                    |
| innodb_log_checksums                    | ON                                          |
| innodb_log_compressed_pages             | ON                                          |
| innodb_log_file_size                    | 50331648                                    |
| innodb_log_files_in_group               | 2                                           |
| innodb_log_group_home_dir               | ./                                          |
| innodb_log_write_ahead_size             | 8192                                        |
| innodb_max_undo_log_size                | 1073741824                                  |
| innodb_online_alter_log_max_size        | 134217728                                   |
| innodb_undo_log_truncate                | OFF                                         |
| innodb_undo_logs                        | 128                                         |
| log_bin                                 | OFF                                         |
| log_bin_basename                        |                                             |
| log_bin_index                           |                                             |
| log_bin_trust_function_creators         | OFF                                         |
| log_bin_use_v1_row_events               | OFF                                         |
| log_builtin_as_identified_by_password   | OFF                                         |
| log_error                               | ./bogon.err                                 |
| log_error_verbosity                     | 3                                           |
| log_output                              | FILE                                        |
| log_queries_not_using_indexes           | OFF                                         |
| log_slave_updates                       | OFF                                         |
| log_slow_admin_statements               | OFF                                         |
| log_slow_slave_statements               | OFF                                         |
| log_statements_unsafe_for_binlog        | ON                                          |
| log_syslog                              | OFF                                         |
| log_syslog_facility                     | daemon                                      |
| log_syslog_include_pid                  | ON                                          |
| log_syslog_tag                          |                                             |
| log_throttle_queries_not_using_indexes  | 0                                           |
| log_timestamps                          | UTC                                         |
| log_warnings                            | 2                                           |
| max_binlog_cache_size                   | 18446744073709547520                        |
| max_binlog_size                         | 1073741824                                  |
| max_binlog_stmt_cache_size              | 18446744073709547520                        |
| max_relay_log_size                      | 0                                           |
| relay_log                               |                                             |
| relay_log_basename                      | /usr/local/mysql/data/bogon-relay-bin       |
| relay_log_index                         | /usr/local/mysql/data/bogon-relay-bin.index |
| relay_log_info_file                     | relay-log.info                              |
| relay_log_info_repository               | FILE                                        |
| relay_log_purge                         | ON                                          |
| relay_log_recovery                      | OFF                                         |
| relay_log_space_limit                   | 0                                           |
| slow_query_log                          | OFF                                         |
| slow_query_log_file                     | /usr/local/mysql/data/bogon-slow.log        |
| sql_log_bin                             | ON                                          |
| sql_log_off                             | OFF                                         |
| sync_binlog                             | 1                                           |
| sync_relay_log                          | 10000                                       |
| sync_relay_log_info                     | 10000                                       |
+-----------------------------------------+---------------------------------------------+
```

