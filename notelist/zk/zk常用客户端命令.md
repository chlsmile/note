## zk常用客户端命令

| 命令  | 功能  | 语法格式 | 样例 |
|------------- |---------------| -------------| -------------|
| help     | 列出客户端支持的功能 |  help                                |[zk: localhost:2181(CONNECTED) 7] help |
| ls       | 查看节点结构        |  ls path [watch]                     | [zk: localhost:2181(CONNECTED) 1] ls /|
| create   | 创建节点            |  create [-s] [-e] path data acl      | [zk: localhost:2181(CONNECTED) 2] create /zk_test my_data|
| get      | 查看节点数据        |  get path [watch]                    | [zk: localhost:2181(CONNECTED) 3] get /zk_test|
| set      | 变更节点数据        |  set path data [version]             |[zk: localhost:2181(CONNECTED) 4] set /zk_test junk |
| delete   | 删除节点            |  delete path [version]               |[zk: localhost:2181(CONNECTED) 8] delete /zk_test |










