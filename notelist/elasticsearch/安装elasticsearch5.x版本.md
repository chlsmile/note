## 安装elasticsearch5.X版本
###简介
> 安装elasticsearch5.X版本后需要使用非root用户启动，同时需要修改一些服务器配置参数，否则启动会失败

###安装
```
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.1.tar.gz

tar -xvf elasticsearch-5.4.1.tar.gz
```
###修改jvm heap基础配置信息
elasticsearch5.X版本默认的-Xms与-Xms值得大小均为2GB,可以根据实际机器状况调整这两个参数，由于采用虚拟机测试配置较低，所以修改这两个值均为1GB

```
文件所在位置$ELASTICSEARCH_HOME/conf/jvm.options

修改前
# Xms represents the initial size of total heap space
# Xmx represents the maximum size of total heap space

-Xms2g
-Xmx2g

修改后
# Xms represents the initial size of total heap space
# Xmx represents the maximum size of total heap space

-Xms1g
-Xmx1g

```

###修改elasticsearch.yml基础配置信息
```
1.修改集群名
#cluster.name: my-application
cluster.name: es-cluster-demo

2.修改节点名
#node.name: node-1
node.name: es-node-1

3.修改存储数据路径
#path.data: /path/to/data
path.data: /home/esdev/elasticsearch-5.4.1/data

4.修改日志文件路径
#path.logs: /path/to/logs
path.logs: /home/esdev/elasticsearch-5.4.1/logs


```

###启动elasticsearch(以守护进行的方式启动)
出于安全考虑，elasticsearch5.X版本，要求以非root用户启动

- 启动方式1: 普通启动

```
./elasticsearch
```

- 启动方式2: 以守护进程方式启动

```
./elasticsearch -d
```

###启动报错与解决方案
- 启动时可能会出现如下错误

```
[2] bootstrap checks failed
[1]: max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536]
[2]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
```

- 报错解决方案

```
1.对启动es服务的用户修改硬限制，需要修改的文件/etc/security/limits.conf，增加如下内容
esdev soft nofile 65536
esdev hard nofile 65536

2.退出用户重新登录，使配置生效
[esdev@redhat1 bin]$ exit

3.修改/etc/sysctl.conf文件，增加如下内容
vm.max_map_count=655360

4.保存后执行
[root@redhat1 ~]# sysctl -p

```




