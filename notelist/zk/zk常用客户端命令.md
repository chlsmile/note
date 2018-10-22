## zk常用客户端命令

### help
功能  | 语法格式
------------- | -------------
列表客户端可以执行的命令  | help

#### 样例
```bash
[zk: localhost:2181(CONNECTED) 0] help
ZooKeeper -server host:port cmd args
	stat path [watch]
	set path data [version]
	ls path [watch]
	delquota [-n|-b] path
	ls2 path [watch]
	setAcl path acl
	setquota -n|-b val path
	history
	redo cmdno
	printwatches on|off
	delete path [version]
	sync path
	listquota path
	rmr path
	get path [watch]
	create [-s] [-e] path data acl
	addauth scheme auth
	quit
	getAcl path
	close
	connect host:port
```

### ls
功能  | 语法格式
------------- | -------------
查看节点结构  | ls path [watch]

#### 样例
```bash
[zk: localhost:2181(CONNECTED) 1] ls /
[zookeeper]
```

### create

功能  | 语法格式
------------- | -------------
创建节点  | create [-s] [-e] path data acl

#### 样例
```bash
[zk: localhost:2181(CONNECTED) 2] create /zk_test my_data
Created /zk_test
```

### get
功能  | 语法格式
------------- | -------------
查看节点数据  | get path [watch]

#### 样例
```bash
[zk: localhost:2181(CONNECTED) 3] get /zk_test
my_data
cZxid = 0x10000000f
ctime = Mon Oct 22 14:46:16 CST 2018
mZxid = 0x10000000f
mtime = Mon Oct 22 14:46:16 CST 2018
pZxid = 0x10000000f
cversion = 0
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 7
numChildren = 0
```

### set
功能  | 语法格式
------------- | -------------
变更节点数据  | set path data [version]

#### 样例
```bash
[zk: localhost:2181(CONNECTED) 4] set /zk_test junk
cZxid = 0x10000000f
ctime = Mon Oct 22 14:46:16 CST 2018
mZxid = 0x100000010
mtime = Mon Oct 22 14:50:07 CST 2018
pZxid = 0x10000000f
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 4
numChildren = 0

```

### delete
功能  | 语法格式
------------- | -------------
删除节点  | delete path [version]

#### 样例
```bash
[zk: localhost:2181(CONNECTED) 8] delete /zk_test
```










