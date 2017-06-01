## Elasticsearch安装

#### Elasticsearch与jdk版本

Elasticsearch依赖于jdk，Elasticsearch依赖的jdk版本如下：

Elasticsearch版本  | jdk版本
------------- | -------------
Elasticsearch5.X  | Elasticsearch requires at least Java 8. Specifically as of this writing, it is recommended that you use the Oracle JDK version 1.8.0_73. 
Elasticsearch2.X  | Elasticsearch requires at least Java 7. Specifically as of this writing, it is recommended that you use the Oracle JDK version 1.8.0_25. 
Elasticsearch1.7~ Elasticsearch1.4 | Elasticsearch requires at least Java 7. Specifically as of this writing, it is recommended that you use the Oracle JDK version 1.8.0_25. 
Elasticsearch1.3 | Elasticsearch requires Java 7. Specifically as of this writing, it is recommended that you use the Oracle JDK version 1.7.0_60. 


#### Elasticsearch安装

```
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.0.tar.gz

tar -xvf elasticsearch-5.4.0.tar.gz

cd elasticsearch-5.4.0/bin

./elasticsearch
```

- 如果你想把 Elasticsearch 作为一个守护进程在后台运行，那么可以在后面添加参数 -d 
- 测试 Elasticsearch 是否启动成功，可以打开另一个终端，执行以下操作：curl 'http://localhost:9200/?pretty'



