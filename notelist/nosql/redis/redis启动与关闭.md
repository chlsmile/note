## redis的启动与关闭

### redis的启动

#### 默认启动(默认启动的端口是6379)
- /usr/local/bin/redis-server

#### 指定端口号启动
- /usr/local/bin/redis-server  --port 6380

#### 指定配置文件启动
- /usr/local/bin/redis-server /usr/local/redis-3.2.3/redis.conf

#### 通过启动参数传递同名的配置选项会覆盖配置文件中相应的参数, 例如:
- /usr/local/bin/redis-server /usr/local/redis-3.2.3/redis.conf --loglevel  warning


### redis的关闭

