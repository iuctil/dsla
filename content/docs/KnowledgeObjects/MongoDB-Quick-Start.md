---
title: "MongoDB Quick-Start"
description: "MongoDB Quick-Start"
#lead: "MongoDB Quick-Start"
keywords: 
    - Data Science
    - NoSql
contributors:
    - Leon Hwang 
date: 2022-03-01T00:00:00+00:00
lastmod: 2022-03-19T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---
MongoDB is a document-oriented database and one of the most popular NoSQL databases. It uses JSON-like documents. MongoDB offers both local and cloud-hosted options, called [MongoDB Atlas](https://www.mongodb.com/cloud/atlas?tck=docs_server).

A record in MongoDB is a **document** which is composed of **field-value** pairs similar to JSON objects. MongoDB stores documents in **collections** that is equivalent to tables in relational databases. Internally MongoDB stores a binary representation of JSON known as BSON. This allows MongoDB to provide data types like decimal that are not defined in the JSON specification. For more information on the BSON spec check out the following URL: [http://bsonspec.org](http://bsonspec.org).




##  Basic Commands

MongoDB supports a rich query language to support CRUD operations, data aggregation, text search, as well as geospatial queries.  

The following list shows the various SQL terminology and concepts and the corresponding ones in MongDB. 

- Database -> Database
- Table -> Collection
- Row -> Document
- Column -> Field
- Index -> Index
- Joins -> $lookup (for embedded documents)
- Primary key -> Primary key (in MongoDB, _id field)
- Transactions -> Transactions



MondoDB shell supports the javascript style syntax. Here are some basic commands. You can find more MongoDB methods [here](https://docs.mongodb.com/manual/reference/method/).



### Connect MongoDB Shell

```bash
# connects to mongodb://127.0.0.1:27017 by default
mongo 

# connects to a specific MongoDB server
mongo --host <host> --port <port> -u <user> -p <pwd> 
mongo "mongodb://192.168.1.1:27017"

# connects to MongoDB Atlas
mongo "mongodb+srv://cluster-name.abcde.mongodb.net/<dbname>" --username <username> 
```



### Databases and Collections

```javascript
// prints the current database
show dbs

// switch database
use <database_name>

// removes the collection and its index definitions
db.coll.drop()
db.dropDatabase() 

// show collections
show collection

// create collection with a $jsonschema
db.createCollection("contacts", {
   validator: {$jsonSchema: {
      bsonType: "object",
      required: ["phone"],
      properties: {
         phone: {
            bsonType: "string",
            description: "must be a string and is required"
         },
         email: {
            bsonType: "string",
            pattern: "@mongodb\.com$",
            description: "must be a string and match the regular expression pattern"
         },
         status: {
            enum: [ "Unknown", "Incomplete" ],
            description: "can only be one of the enum values"
         }
      }
   }}
})

// other collection functions
db.coll.stats()
db.coll.storageSize()
db.coll.totalIndexSize()
db.coll.totalSize()
db.coll.validate({full: true})
// rename collection and drop the target collection if exists
db.coll.renameCollection("new_coll", true) 
```



### CRUD

**CREATE**

```javascript
// insert a single record
db.coll.insertOne({name: "Max"})
// ordered bulk insert
db.coll.insert([{name: "Max"}, {name:"Alex"}])
// unordered bulk insert
db.coll.insert([{name: "Max"}, {name:"Alex"}], {ordered: false}) 
// insert date
db.coll.insert({date: ISODate()})
// insert with writeConcern
db.coll.insert({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

**READ**

```javascript
// returns a single document
db.coll.findOne() 
// returns a cursor - show 20 results - "it" to display more
db.coll.find()    
// prettify results
db.coll.find().pretty()
// implicit logical "AND"
db.coll.find({name: "Max", age: 32})
// datetime support
db.coll.find({date: ISODate("2020-09-25T13:57:17.180Z")})
// or "queryPlanner" or "allPlansExecution"
db.coll.find({name: "Max", age: 32}).explain("executionStats") 
// return distinct names
db.coll.distinct("name")

// count estimation based on collection metadata
db.coll.count({age: 32})          
// count estimation based on collection metadata
db.coll.estimatedDocumentCount()
// alias for an aggregation pipeline - accurate count
db.coll.countDocuments({age: 32}) 

// comparison
db.coll.find({"year": {$gt: 1970}})
db.coll.find({"year": {$gte: 1970}})
db.coll.find({"year": {$lt: 1970}})
db.coll.find({"year": {$lte: 1970}})
db.coll.find({"year": {$ne: 1970}})
db.coll.find({"year": {$in: [1958, 1959]}})
db.coll.find({"year": {$nin: [1958, 1959]}})

// logical
db.coll.find({name:{$not: {$eq: "Max"}}})
db.coll.find({$or: [{"year" : 1958}, {"year" : 1959}]})
db.coll.find({$nor: [{price: 1.99}, {sale: true}]})
db.coll.find({
  $and: [
    {$or: [{qty: {$lt :10}}, {qty :{$gt: 50}}]},
    {$or: [{sale: true}, {price: {$lt: 5 }}]}
  ]
})

// element
db.coll.find({name: {$exists: true}})
db.coll.find({"zipCode": {$type: 2 }})
db.coll.find({"zipCode": {$type: "string"}})

// aggregation pipeline
db.coll.aggregate([
  {$match: {status: "A"}},
  {$group: {_id: "$cust_id", total: {$sum: "$amount"}}},
  {$sort: {total: -1}}
])

// text search with a "text" index
db.coll.find(
  {$text: {$search: "cake"}}, {score: {$meta: "textScore"}}).sort(
  {score: {$meta: "textScore"}}
)

// regular expression
db.coll.find({name: /^Max/})   
db.coll.find({name: /^Max$/i}) 

// array
db.coll.find({tags: {$all: ["Realm", "Charts"]}})
// impossible to index - prefer storing the size of the array & update it
db.coll.find({field: {$size: 2}}) 
// element level matching
db.coll.find({results: {$elemMatch: {product: "xyz", score: {$gte: 8}}}})

// projections - actors + _id
db.coll.find({"x": 1}, {"actors": 1})
// projections - actors
db.coll.find({"x": 1}, {"actors": 1, "_id": 0})     
// projections - all but "actors" and "summary"
db.coll.find({"x": 1}, {"actors": 0, "summary": 0}) // 

// sort, skip, limit
db.coll.find({}).sort({"year": 1, "rating": -1}).skip(10).limit(3)

// read concern
db.coll.find().readConcern("majority")
```

**UPDATE**

```javascript
// replaces the entire document
db.coll.update({"_id": 1}, {"year": 2016})
// set specific fields
db.coll.update({"_id": 1}, {$set: {"year": 2016, name: "Max"}})
// unset specific fields
db.coll.update({"_id": 1}, {$unset: {"year": 1}})
// rename fields
db.coll.update({"_id": 1}, {$rename: {"year": "date"} })
// arithmetic operations
db.coll.update({"_id": 1}, {$inc: {"year": 5}})
db.coll.update({"_id": 1}, {$mul: {price: NumberDecimal("1.25"), qty: 2}})
db.coll.update({"_id": 1}, {$min: {"imdb": 5}})
db.coll.update({"_id": 1}, {$max: {"imdb": 8}})
// datetime operations
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": true}})
db.coll.update({"_id": 1}, {$currentDate: {"lastModified": {$type: "timestamp"}}})

// array
db.coll.update({"_id": 1}, {$push :{"array": 1}})
db.coll.update({"_id": 1}, {$pull :{"array": 1}})
db.coll.update({"_id": 1}, {$addToSet :{"array": 2}})
// last element
db.coll.update({"_id": 1}, {$pop: {"array": 1}})
// first element
db.coll.update({"_id": 1}, {$pop: {"array": -1}}) 
db.coll.update({"_id": 1}, {$pullAll: {"array" :[3, 4, 5]}})
db.coll.update({"_id": 1}, {$push: {scores: {$each: [90, 92, 85]}}})
db.coll.updateOne({"_id": 1, "grades": 80}, {$set: {"grades.$": 82}})
db.coll.updateMany({}, {$inc: {"grades.$[]": 10}})
db.coll.update(
  {}, 
  {$set: {"grades.$[element]": 100}}, 
  {multi: true, arrayFilters: [{"element": {$gte: 100}}]}
)

// update many
db.coll.update({"year": 1999}, {$set: {"decade": "90's"}}, {"multi":true})
db.coll.updateMany({"year": 1999}, {$set: {"decade": "90's"}})

// find one and update
db.coll.findOneAndUpdate(
  {"name": "Max"}, 
  {$inc: {"points": 5}}, {returnNewDocument: true}
)

// upsert
db.coll.update(
  {"_id": 1}, 
  {$set: {item: "apple"}, $setOnInsert: {defaultQty: 100}}, {upsert: true}
)

// replace
db.coll.replaceOne({"name": "Max"}, {"firstname": "Maxime", "surname": "Beugnet"})

// save
db.coll.save({"item": "book", "qty": 40})

// write concern
db.coll.update({}, {$set: {"x": 1}}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
```

**DELETE**

```javascript
db.coll.remove({name: "Max"})
db.coll.remove({name: "Max"}, {justOne: true})
// deletes all the docs but not the collection itself and its index definitions
db.coll.remove({})
db.coll.remove({name: "Max"}, {"writeConcern": {"w": "majority", "wtimeout": 5000}})
db.coll.findOneAndDelete({"name": "Max"})
```



### Aggregation

Aggregation operates on multiple documents and returns computed results such as the total, average, min/max values, etc.. To perform aggregation operations, you can use aggregation pipelines or single purpose aggregation methods.



**Single Purpose Aggregation Methods**

The single purpose aggregation methods aggregate documents from a single collection. The methods are simple but lack the capabilities of an aggregation pipeline. For example,

- estimatedDocumentCount(): returns an approximate count of the documents in a collection or a view.
- count(): returns a count of the number of documents in a collection or a view.
- distinct(): returns an array of documents that have distinct values for the specified field.



**Aggregation Pipelines**

An aggregation pipeline consists of one or more stages that process documents. The following code filters the pizza order documents to pizzas with a size of medium, groups them by pizza name, and calculate the total order quantity for each pizza name. 

```javascript
// orders collection
db.orders.insertMany( [
   { _id: 0, name: "Pepperoni", size: "small", price: 19,
     quantity: 10, date: ISODate( "2021-03-13T08:14:30Z" ) },
   { _id: 1, name: "Pepperoni", size: "medium", price: 20,
     quantity: 20, date : ISODate( "2021-03-13T09:13:24Z" ) },
   { _id: 2, name: "Pepperoni", size: "large", price: 21,
     quantity: 30, date : ISODate( "2021-03-17T09:22:12Z" ) },
   { _id: 3, name: "Cheese", size: "small", price: 12,
     quantity: 15, date : ISODate( "2021-03-13T11:21:39.736Z" ) },
   { _id: 4, name: "Cheese", size: "medium", price: 13,
     quantity:50, date : ISODate( "2022-01-12T21:23:13.331Z" ) },
   { _id: 5, name: "Cheese", size: "large", price: 14,
     quantity: 10, date : ISODate( "2022-01-12T05:08:13Z" ) },
   { _id: 6, name: "Vegan", size: "small", price: 17,
     quantity: 10, date : ISODate( "2021-01-13T05:08:13Z" ) },
   { _id: 7, name: "Vegan", size: "medium", price: 18,
     quantity: 10, date : ISODate( "2021-01-13T05:10:13Z" ) }
] )
```

```javascript
db.orders.aggregate( [
   // Stage 1: Filter pizza order documents by pizza size
   {$match: { size: "medium" }},
   // Stage 2: Group remaining documents by pizza name and calculate total quantity
   {$group: { _id: "$name", totalQuantity: { $sum: "$quantity" }}}])

// Example output
[
   { _id: 'Cheese', totalQuantity: 50 },
   { _id: 'Vegan', totalQuantity: 10 },
   { _id: 'Pepperoni', totalQuantity: 20 }
]
```

The following example calculates the total pizza order value and average order quantity between two dates

```javascript
db.orders.aggregate( [
   // Stage 1: Filter pizza order documents by date range
   {$match: {
       "date": { $gte: new ISODate("2020-01-30"), $lt: new ISODate("2022-01-30") }
   }},
   // Stage 2: Group remaining documents by date and calculate results
   {$group: {
       _id: { $dateToString: { format: "%Y-%m-%d", date: "$date" } },
       totalOrderValue: { $sum: { $multiply: [ "$price", "$quantity" ] } },
       averageOrderQuantity: { $avg: "$quantity" }
   }},
   // Stage 3: Sort documents by totalOrderValue in descending order
   {$sort: { totalOrderValue: -1 }}
 ] )

// Example ouptut
[
   { _id: '2022-01-12', totalOrderValue: 790, averageOrderQuantity: 30 },
   { _id: '2021-03-13', totalOrderValue: 770, averageOrderQuantity: 15 },
   { _id: '2021-03-17', totalOrderValue: 630, averageOrderQuantity: 30 },
   { _id: '2021-01-13', totalOrderValue: 350, averageOrderQuantity: 10 }
]
```



### Indexes

Indexes are a small portion of the collection's data set in an easy to traverse form to support the efficient execution of queries in MongoDB. The index stores the value of a specific field or set of fields, ordered by the value of the field. By default, MongoDB creates the `_id` index during the creation of a collection and you cannot drop this index. To create an index, you use `db.collection.createIndex()`, and `db.collection.getIndexes()` to get indexes.



**Single Field Index**

```javascript
// create a single field index on the name field
// if an index of the same specification does not already exist. 
// -1 means descending order
db.collection.createIndex( { name: -1 } )
```



**Compound Index**

```javascript
// create a compound index with the name item_1_quantity_-1
db.products.createIndex(
  { item: 1, quantity: -1 }
}

// create a compound index with a custom name
db.products.createIndex(
  { item: 1, quantity: -1 } ,
  { name: "query for inventory" }
)
```



**Multikey Index**

```javascript
// create a multikey index on array fields. For example, 
// ratings: [ 2, 5, 9 ]
// stock: [{ size: "M", color: "blue", quantity: 15 }]
db.products.createIndex( { ratings: 1 } )
db.products.createIndex( { "stock.size": 1, "stock.quantity": 1 } )
```



**Geospartial Index**

Geospartial indexes support efficient queries of geospatial coordinate data.

```javascript
// create a document with the loc field with coordinates
db.places.insert({
      loc : { type: "Point", coordinates: [ -73.97, 40.77 ] },
      name: "Central Park",
      category : "Parks"})

// create a 2dsphere index on the loc field
db.places.createIndex( { loc : "2dsphere" } )

// create a compound index with 2dsphere
db.places.createIndex( { loc : "2dsphere" , category : -1, name: 1 } )
```



**Text Index**

Text indexes support searching for string content in a collection. These text indexes do not store language-specific *stop* words (e.g. "the", "a", "or") and *stem* the words in a collection to only store root words.

```javascript
// create an index on the comments field
db.reviews.createIndex( { comments: "text" } )

// create an index on multiple fields
db.reviews.createIndex( { subject: "text", comments: "text" } )

// create an index on multiple fields with different weights
// the default weight is 1 if not specified
db.reviews.createIndex( 
  { subject: "text", comments: "text" },
  { weights: { subject: 5, comments: 2}, name: "TextIndex" } 
)

// create an index on multiple fields using the wildcard specifier
db.collection.createIndex( { "$**": "text" } )
```



**Hashed Index**

Hashed indexes maintain entries with hashes of the values of the indexed field and support sharing using hashed shard keys. 

```javascript
// single hashed index
db.collection.createIndex( { _id: "hashed" } )

// compound hashed index
db.collection.createIndex( { "fieldA" : 1, "fieldB" : "hashed", "fieldC" : -1 } )
```



**Unique Index**

The unique index property for an index causes MongoDB to reject duplicate values for the indexed field. 

```javascript
// user_id must be unique
db.members.createIndex( { "user_id": 1 }, { unique: true } )

// unique compound index
db.members.createIndex( { groupNumber: 1, lastname: 1, firstname: 1 }, { unique: true } )
```



**Partial Index**

Partial indexes only index the documents in a collection that meet a specified filter expression. By indexing a subset of the documents in a collection, partial indexes have lower storage requirements and reduced performance costs for index creation and maintenance.

```javascript
// creates a compound index that indexes only the documents 
// with a rating field greater than 5.
db.restaurants.createIndex(
   { cuisine: 1, name: 1 },
   { partialFilterExpression: { rating: { $gt: 5 } } }
)
```



**TTL Index**

TTL indexes expire documents after the specified number of seconds has passed since the indexed field value; i.e. the expiration threshold is the indexed field value plus the specified number of seconds. If the field is an array, and there are multiple date values in the index, MongoDB uses *lowest* (i.e. earliest) date value in the array to calculate the expiration threshold. If the indexed field in a document is not a date or an array that holds one or more date values, the document will not expire. If a document does not contain the indexed field, the document will not expire.

```javascript
// remove expired documents after 3600 seconds
db.eventlog.createIndex( { "lastModifiedDate": 1 }, { expireAfterSeconds: 3600 } )
```



**Hidden Index**

By hiding an index from the planner, users can evaluate the potential impact of dropping an index without actually dropping the index. If the impact is negative, the user can unhide the index instead of having to recreate a dropped index. Except for the `_id` index, you can hide any indexes.

```javascript
// creates a hidden ascending index on the borough field
db.addresses.createIndex(
   { borough: 1 },
   { hidden: true }
);

// hide an existing index
db.restaurants.hideIndex( { borough: 1 } )

// you can also use the index name
db.restaurants.hideIndex( "borough_1" )
```



## References

1. https://en.wikipedia.org/wiki/MongoDB
2. https://www.mongodb.com/docs/manual/reference/sql-comparison/
3. https://www.mongodb.com/developer/quickstart/cheat-sheet/
4. https://docs.mongodb.com/manual/crud/
5. https://docs.mongodb.com/manual/reference/method/
6. https://docs.mongodb.com/manual/reference/operator/
7. https://docs.mongodb.com/manual/aggregation/
8. https://www.mongodb.com/docs/manual/reference/operator/aggregation-pipeline/
9. https://www.mongodb.com/docs/manual/indexes/
10. https://www.mongodb.com/docs/manual/core/index-sparse/
11. https://www.mongodb.com/docs/manual/core/index-text/
12. https://www.mongodb.com/docs/manual/core/index-hashed/
13. https://www.mongodb.com/docs/manual/core/index-ttl/
14. https://www.mongodb.com/docs/manual/core/index-hidden/
