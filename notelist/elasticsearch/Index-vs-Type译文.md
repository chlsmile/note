## Elasticsearch中Index与Type对比(译文)

Who has never wondered whether new data should be put into a new type of an existing index, or into a new index? This is a recurring question for new users, that can’t be answered without understanding how both are implemented.


In the past we tried to make elasticsearch easier to understand by building an analogy with relational databases: indices would be like a database, and types like a table in a database. This was a mistake: the way data is stored is so different that any comparisons can hardly make sense, and this ultimately led to an overuse of types in cases where they were more harmful than helpful.

### What is an index?
An index is stored in a set of shards, which are themselves Lucene indices. This already gives you a glimpse of the limits of using a new index all the time: Lucene indices have a small yet fixed overhead in terms of disk space, memory usage and file descriptors used. For that reason, a single large index is more efficient than several small indices: the fixed cost of the Lucene index is better amortized across many documents.

Another important factor is how you plan to search your data. While each shard is searched independently, Elasticsearch eventually needs to merge results from all the searched shards. For instance if you search across 10 indices that have 5 shards each, the node that coordinates the execution of a search request will need to merge 5x10=50 shard results. Here again you need to be careful: if there are too many shard results to merge and/or if you ran an heavy request that produces large shard responses (which can easily happen with aggregations), the task of merging all these shard results can become very resource-intensive, both in terms of CPU and memory. Again this would advocate for having fewer indices.


### What is a type?
This is where types help: types are a convenient way to store several types of data in the same index, in order to keep the total number of indices low for the reasons exposed above. In terms of implementation it works by adding a “_type” field to every document that is automatically used for filtering when searching on a specific type. One nice property of types is that searching across several types of the same index comes with no overhead compared to searching a single type: it does not change how many shard results need to be merged.


However this comes with limitations as well:

- Fields need to be consistent across types. For instance if two fields have the same name in different types of the same index, they need to be of the same field type (string, date, etc.) and have the same configuration.

- Fields that exist in one type will also consume resources for documents of types where this field does not exist. This is a general issue with Lucene indices: they don’t like sparsity. Sparse postings lists can’t be compressed efficiently because of high deltas between consecutive matches. And the issue is even worse with doc values: for speed reasons, doc values often reserve a fixed amount of disk space for every document, so that values can be addressed efficiently. This means that if Lucene establishes that it needs one byte to store all value of a given numeric field, it will also consume one byte for documents that don’t have a value for this field. Future versions of Elasticsearch will have improvements in this area but I would still advise you to model your data in a way that will limit sparsity as much as possible.

- Scores use index-wide statistics, so scores of documents in one type can be impacted by documents from other types.

This means types can be helpful, but only if all types from a given index have mappings that are similar. Otherwise, the fact that fields also consume resources in documents where they don’t exist could make things worse than if the data had been stored in separate indices.


### Which one should I use?

This is a tough question, and the answer will depend on your hardware, data and use-case. First it is important to realize that types are useful because they can help reduce the number of Lucene indices that Elasticsearch needs to manage. But there is another way that you can reduce this number: creating indices that have fewer shards. For instance, instead of folding 5 types into the same index, you could create 5 indices with 1 primary shard each.

I will try to summarize the questions you should ask yourself to make a decision:

- Are you using parent/child? If yes this can only be done with two types in the same index.

- Do your documents have similar mappings? If no, use different indices.

- If you have many documents for each type, then the overhead of Lucene indices will be easily amortized so you can safely use indices, with fewer shards than the default of 5 if necessary

- Otherwise you can consider putting documents in different types of the same index. Or even in the same type.

In conclusion, you may be surprised that there are not as many use cases for types as you expected. And this is right: there are actually few use cases for having several types in the same index for the reasons that we mentioned above. Don’t hesitate to allocate different indices for data that would have different mappings, but still keep in mind that you should keep a reasonable number of shards in your cluster, which can be achieved by reducing the number of shards for indices that don’t require a high write throughput and/or will store low numbers of documents.



### 原文连接

[index-vs-type](<https://www.elastic.co/blog/index-vs-type>)

https://github.com/elastic/elasticsearch/pull/24317