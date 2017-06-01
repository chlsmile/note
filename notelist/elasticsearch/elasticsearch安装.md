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

- Let’s download the Elasticsearch 5.4.0 tar as follows (Windows users should download the zip package):

```
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.0.tar.gz
```

- Then extract it as follows (Windows users should unzip the zip package):

```
tar -xvf elasticsearch-5.4.0.tar.gz	
```

- It will then create a bunch of files and folders in your current directory. We then go into the bin directory as follows:

```
cd elasticsearch-5.4.0/bin
```

- And now we are ready to start our node and single cluster (Windows users should run the elasticsearch.bat file):

```
./elasticsearch
```


