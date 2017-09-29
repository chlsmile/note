## elasticsearch常用rest-api

#### 对集群的基本操作

```
# 查询集群健康
curl -XGET 'http://virtual.es.com/_cat/health?v&pretty'

# 查询节点信息
curl -XGET 'http://virtual.es.com/_cat/nodes?v&pretty'

# 查询集群所有索引信息
curl -XGET 'http://virtual.es.com/_cat/indices?v&pretty'



```

#### 对索引操作

```
# 创建索引(索引在默认情况下会被分配5个主分片,1个副本分片)
curl -XPUT 'http://virtual.es.com/customer?pretty&pretty'


# 创建索引(指定主分片与副本分片数)
curl -XPUT 'http://virtual.es.com/audi?pretty' -H 'Content-Type: application/json' -d'
{
   "settings" : {
      "number_of_shards" : 3,
      "number_of_replicas" : 1
   }
}
'


# 删除一个索引
curl -XDELETE 'http://virtual.es.com/customer?pretty&pretty'
```

#### 对文档的操作-新增
```


# 索引一条文档(自定义id)
curl -XPUT 'lhttp://virtual.es.com/customer/external/1?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "name": "John Doe"
}
'

# 对文档的操作-索引一条文档(非自定id)
curl -XPOST 'http://virtual.es.com/customer/external?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "name": "Jane Doe"
}
'

# 对文档的操作-批量索引文档
curl -XPOST 'http://virtual.es.com/customer/external/_bulk?pretty&pretty' -H 'Content-Type: application/json' -d'
{"index":{"_id":"1"}}
{"name": "John Doe" }
{"index":{"_id":"2"}}
{"name": "Jane Doe" }
'


```

#### 对文档的操作-修改

```
# 根据id修改文档
curl -XPUT 'http://virtual.es.com/customer/external/1?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "name": "Jane Doe"
}
'

# 更新一条文档
curl -XPOST 'http://virtual.es.com/customer/external/1/_update?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "doc": { "name": "Jane Doe" }
}
'

# 更新一条文档(增加属性)
curl -XPOST 'lhttp://virtual.es.com/customer/external/1/_update?pretty&pretty' -H 'Content-Type: application/json' -d'
{
  "doc": { "name": "Jane Doe", "age": 20 }
}
'
```

#### 对文档的操作-删除

```
# 删除一条文档
curl -XDELETE 'http://virtual.es.com/customer/external/2?pretty&pretty'
```

#### 对文档的操作-查询

```
# 根据id查询一条文档
curl -XGET 'http://virtual.es.com/customer/external/1?pretty&pretty'

# 查询所有
curl -XGET 'http://virtual.es.com/bank/_search?q=*&sort=account_number:asc&pretty&pretty'

# 查询所有
curl -XGET 'http://virtual.es.com/bank/_search?pretty' -H 'Content-Type: application/json' -d'
{
  "query": { "match_all": {} },
  "sort": [
    { "account_number": "asc" }
  ]
}
'


```






