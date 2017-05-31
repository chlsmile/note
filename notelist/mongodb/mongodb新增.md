## mongodb Insert Methods
MongoDB provides the following methods for inserting documents into a collection:


方法  | 说明 | 备注
------------- | ------------- | -------------
db.collection.insertOne()  | Inserts a single document into a collection. | New in version 3.2
db.collection.insertMany()  | db.collection.insertMany() inserts multiple documents into a collection. | New in version 3.2
db.collection.insert()  | db.collection.insert() inserts a single document or multiple documents into a collection. | 


#### db.collection.insert()

- Inserts a document or documents into a collection.

- The insert() method has the following syntax:

- Changed in version 2.6.

```
db.collection.insert(
   <document or array of documents>,
   {
     writeConcern: <document>,
     ordered: <boolean>
   }
)
```

Parameter  | Type | Description
------------- | ------------- | -------------
document  | document or array | A document or array of documents to insert into the collection.
writeConcern  | document | Optional. A document expressing the write concern. Omit to use the default write concern. See Write Concern.New in version 2.6.
ordered  | boolean | 	Optional. If true, perform an ordered insert of the documents in the array, and if an error occurs with one ofdocuments, MongoDB will return without processing the remaining documents in the array. If false, perform an unordered insert, and if an error occurs with one of documents, continue processing the remaining documents in the array. Defaults to true. New in version 2.6







