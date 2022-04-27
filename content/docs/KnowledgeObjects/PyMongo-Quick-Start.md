---
title: "PyMongo Quick-Start"
description: "PyMongo Quick-Start"
#lead: "PyMongo Quick-Start"
keywords: 
    - Data Science
    - NoSql
contributors:
    - Leon Hwang 
date: 2022-04-19T00:00:00+00:00
lastmod: 2022-04-19T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---

Although there are other drivers written by the community, PyMongo is the official Python driver for MongoDB and is one of the most popular. You can install PyMongo with the pip package management system like `pip install pymongo`.



A record in MongoDB is a **document** which is composed of **field-value** pairs similar to JSON objects. MongoDB stores documents in **collections** that is equivalent to tables in relational databases. The following table shows the JSON object types and the corresponding Python object types.



![alt JSON <> Python <> MongoDB](/images/JSON-Python-MongoDB.png)





## Using PyMongo



**Connection**

```python
from pymongo import MongoClient

# default host and port
client = MongoClient() 
# specify host and port
client = MongoClient('localhost', 27017) 
# use URI
client = MongoClient('mongodb://localhost:27017/')
```



**Getting a Database**

```python
# access db using attribute style
db = client.test_database
# the following won't work with attribute style because of `-`
# access db using dictionary style
db = client['test-database']
```



**Getting a Collection**

```python
# list all of the collections in the database
db.list_collection_names()

# access db using attribute style
collection = db.test_collection
# the following won't work with attribute style because of `-`
# access db using dictionary style
collection = db['test-collection']
```



### CRUD

**CREATE**

```python
import datetime

# insert single document
post = {
  "author": "Mike",
  "text": "My first blog post!",
  "tags": ["mongodb", "python", "pymongo"],
  # pymongo converts native python types to/from the appropriate BSON types
  "date": datetime.datetime.utcnow()}

# posts is the collection
posts.insert_one(post)

# insert multiple documents
bulk_post = [{
  "author": "Mike",
  "text": "My first blog post!",
  "tags": ["mongodb", "python", "pymongo"],
  "date": datetime.datetime.utcnow()}, {
  "author": "Bob",
  "text": "I love MongoDB",
  "tags": ["mongodb"],
  "date": datetime.datetime.utcnow()}]  

posts.insert_many([post])
```

**READ**

```python
# returns a single document matching a query
# None if no match is found
posts.find_one()
posts.find_one({"author": "Mike"})

# `_id` is a special value in ObjectId
# if post_id is already an ObjectId
posts.find_one({"_id": post_id}) 
# if post_id is not an ObjectId
posts.find_one({"_id": ObjectId(post_id)})
# `_id` is not a string
posts.find_one({"_id": str(post_id)}) # No result

# returns multiple documents
# `find` returns a cursor instance
for post in posts.find({"author": "Mike"}): 
	print(post)

# counting
posts.count_documents({})
posts.count_documents({"author": "Mike"})
# value in a range: `$in`
posts.count_documents({"author": {"$in": ["Mike", "Bob"]}})
# not equal: `$ne`
posts.count_documents({"author": {"$ne": "Mike"}})

# advanced queries
# `$lt` means less than
for post in posts.find(
  		{"date": {"$lt": datetime.datetime(2009, 11, 12, 12)}}
		).sort("author"):
  print(post)
```

**UPDATE**

```python
# update one document
result = posts.update_one(
  {"author": "Mike"},
	{"text": "Hellp PyMongo!"})

print(result.matched_count) # returns 1
print(result.modified_count) # returns 1

# returns the original version of the document
result = posts.find_one_and_update(
  {"author": "Mike"},
	{"text": "Hellp PyMongo!"})

# returns the updated version of the document
result = posts.find_one_and_update(
  {"author": "Mike"},
	{"text": "Hellp PyMongo!"},
	return_document=ReturnDocument.AFTER)

# update if found; otherwise, insert a new document
result = posts.update_one(
  {"author": "Mike"},
	{"text": "Hellp PyMongo!"},
	upsert=True)

# update all documents that `author` is `Mike`
result = posts.update_many(
  {"author": "Mike"},
	{"text": "Hellp PyMongo!"})
```

**DELETE**

```python
# delete one document
posts.delete_one({"author": "Mike"})

# delete all documents that `author` is `Mike`
posts.delete_many({"author": "Mike"})
```



## Aggregation

Aggregation operates on multiple documents and returns computed results such as the total, average, min/max values, etc.. For example, the following code filters the pizza order documents to pizzas with a size of medium, groups them by pizza name, and calculate the total order quantity for each pizza name. 

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

The following example calculates the total pizza order value and average order quantity between two dates.

```javascript
db.orders.aggregate( [
   // Stage 1: Filter pizza order documents by date range
   {$match: {
       "date": { $gte: new ISODate( "2020-01-30" ), $lt: new ISODate( "2022-01-30" ) }
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

### Using Aggregation with Python

```python
# Aggregate
cursor = db.laureates.aggregate([
  {"$match": {"bornCountry": "USA"}},
  {"$project": {"prizes.year": 1}},
  {"$limit": 3}
) ])

# Access the aggregation result via the cursor
for doc in cursor:
  print(doc["prizes"])
  
# Example output
[{'year': '1923'}]
[{'year': '1927'}]
[{'year': '1936'}]
```

```python
# Adding sort and skip
from collections import OrderedDict

list(db.laureates.aggregate([
    {"$match": {"bornCountry": "USA"}},
    {"$project": {"prizes.year": 1, "_id": 0}},
    {"$sort": OrderedDict([("prizes.year", 1)])},
    {"$skip": 1},
    {"$limit": 3}
]))

# Example output
[{'prizes': [{'year': '1912'}]},
 {'prizes': [{'year': '1914'}]},
 {'prizes': [{'year': '1919'}]}]
```

```python
# Multi-parameter operator expression
db.laureates.aggregate([
    {"$project": {"solo_winner": {"$in": ["1", "$prizes.share"]}}}
]).next()

# Example output
{'_id': ObjectId('5bd3a610053b1704219e19d4'), 'solo_winner': True}
```



## References

1. https://www.mongodb.com/blog/post/getting-started-with-python-and-mongodb
2. https://pymongo.readthedocs.io/en/stable/tutorial.html
3. https://pymongo.readthedocs.io/en/stable/api/pymongo/collection.html
