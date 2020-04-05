- [MongoDB](https://docs.mongodb.com/manual/introduction/)
- A **document** is a record in a MongoDB collection and the basic unit of data in MongoDB.
- Documents are analogous to JSON objects or records in an relational database, consisting of {name:value} pairs.

- MongoDB stores documents in **collections** (analogous to tables in relational databases). 
- While the documents in a collection are usually similar or related to each other, they can have different fields.
- The values of fields in a document may include other documents, arrays, and arrays of documents. 

- If a collection does not exist, MongoDB creates the collection when you first store data for that collection.
- A **collection** is a group of documents (usually the documents in a collection are similar or related to each other) and is equivalent to a table in a relational database.
- There is no schema in a NoSQL database such as MongoDB. Each document can store whatever is applicable to it.
- A number of **databases** can be run on a single MongoDB server.


  ## MongoDB database and collection commands.  
- `show dbs` : Show databases
- `use <db>` : Switch to a database if it exists. If it does't already exist, MongoDB creates a new database.
- `db` : to show current database (like `select database`)
- `show collections` : to show collections in the current database (like `show tables`)
- a database will not show in the list of databases returned from `show dbs` unless there is at least one document inserted into it
- `db.dropDatabase()` method to delete a database. First need to use `use <database>`  to switch to the database. 

- `db.collection_name.drop()`  to drop or delete a collection
- `db.docs.drop()` to drop a collection called docs from the current database. 

## Creating Documents:

- a document must have an `_id` field. If one isn't provided, MongoDB will automatically generate a unique one.
- The `_id` attribute ensures the uniqueness of every document.
- The `_id` cannot be an array.
- to create a document, call the `save()` method, passing in the document. 
- `db.collection.save()` where `db` is not the name of a database but refers to the current database.

- `db.collection.insert()` to add a document to a collection.
- `db.collection.insertOne()` to 

- The `save` method is actually a wrapper method which calls one of two method `insert` or `update`. 

- If you pass a document id to the `save` method where the id already exists, it overwrites the existing document. 

- `insert()` method to insert a document or documents into a collection.

- To insert multiple documents, pass them to the `insert` method in an array. (an ordered collection of data in square brackets). The attributes of each document do not have to be the same.

- `db.collection.insertOne(document)` to insert just one document into a collection

- See [`db.collection.insertMany()`](https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#db.collection.insertMany) for inserting multiple documents into a collection. 
- `db.collection.insertMany()` method takes an array of documents.

- `db.createCollection(name, options)` can be used to create a collection but a collection is created automatically when a document is inserted.

- `show collections `


- `db.docs.save( {_id:121, first_name : "John", surname : "Smith", email :"johnsm@gmail.com", age: 23})`

See [collection methods manual](https://docs.mongodb.com/manual/reference/method/js-collection/#collection-methods) for a list of all Mongo shell Collection methods.


# Querying the database: The `find()` method.

- `db.collection.find()` to find all documents from a collection called collection in the current database.
- equivalent to `SELECT * FROM collection`

- `db.collection.find(query, projection)`

- The `find()` method is used to query data from a MongoDB collection.
-  `db.collection.find()` method to select the documents from a collection
- The syntax of the find method is `find(query, projection)`.
-  The (optional) `query` parameter is what you are looking for - whatever documents match this query is returned. It is used to narrow down the documents returned.

- The  (optional) `projection` parameter is used to specify which fields are returned in the matching documents (similarly to `select` in MySQL)
- The first set of `{}` provided to the `find` method is the query. - The second set of `{}` is the projection.
- Both the query and projections parameters are optional.
- The `_id` field is always returned unless you specify not to.
- The **projection** determines which fields are returned in the matching documents and is also an optional parameter. (similar to `SELECT` clause in SQL.
- `find()` displays the data in an unstructured way.
- the `pretty()` method can be appended to the `find()` method to return the results in a formatted way. It spaces out name value pairs to make them easier to read by humans.

- `db.collection.find().pretty()`
- `db.collection.find({})` - to select all documents in the collection, passing in an empty document as the query filter document to the method.



- a `query` filter can be used to specify the conditions that determine which records to return.

- The `find` method finds data in a collection. If no parameters are passed (or an empty document) then all documents in the collection will be returned. State which collection and database to find the document in.

- `db.docs.find({})` where db refers to the current database, `docs` is the name of the collection to find the documents in. `find` is the name of the method.

- `db.docs.find().pretty()` 

- `db.docs.findOne()` to only return the first matching document in the database.





## Filtering queries

- The number of documents returned by a `find` can be limited by providing a query to it. The query filter document is like a smaller document. The query is provided in the first set of `{}` to the `find()` method.
- [Query filter documents](https://docs.mongodb.com/manual/core/document/#query-filter-documents) specify the conditions that determine which records to select for read, update, and delete operations.

- `<field> : <value>` expressions can be used to specify an equality condition and [query operator](expressions)

- [All operators](https://docs.mongodb.com/manual/reference/operator/)

- [Update operators](https://docs.mongodb.com/manual/reference/operator/update/%23id1)

- [Logical Query Operators](https://docs.mongodb.com/manual/reference/operator/query-logical/)

- [Comparison Query Operators](https://docs.mongodb.com/manual/reference/operator/query-comparison/)

### Equality matches.
- An equality match is specified as `{<field>:<value>}` to filter the results.
- similar to using the `WHERE` clause in SQL.
- For an equality match (i.e. <field> equals <value>), specify <field>: <value> in the query filter document and pass to the `db.collection.find()` method.

- Equality matches on the embedded document require an exact match, including the field order.
### Equality matches
- `$eq` for equality `{<key>:{$eg;<value>}}`
- `$lt` for less than `{<key>:{$lt:<value>}}`
- `$lte` less than or equal to
- `$gt` greater than
- `$gte` greater than or equal to.
- `$ne` not equal to
- `$in` check for values in an array `<key> : [<value1>, <value2>...<valueN>]
- `$nin` check for values not in an array

- See [query an array](https://docs.mongodb.com/manual/tutorial/query-arrays/). 
on how to specify an equality condition on an array using the query document { <field>: <value> } where <value> is the exact array to match, including the order of the elements.

- `db.docs.find( { colours: ["red", "green"] } )` finds all documents where the field `colours` value is an array with exactly two elements, "red" and "green", in the order as specified.

- `db.docs.find( { colours: { $all: ["red", "green"] } } )` if the order does not matter use the `$all` operator.

### Compound queries using Logical AND, OR query operators 

- These operators can be used to narrow down the results to be more specific. 
- Provide an array of name:value pairs to the `$and` and `$or` operators.
- Provide an array of values to the `$in` operator.

- As MongoDB does not have a schema, some attributes might be common to all documents in the collection but other attributes will be in some documents and not others.
- The `$exists` operator can be used to find documents with specific attributes.

- A compound query can specify conditions for more than one field in the collection’s documents.

- A logical [AND](https://docs.mongodb.com/manual/tutorial/query-documents/#specify-and-conditions) conjunction implicitly connects the clauses of a compound query so that the query selects the documents in the collection that match all the conditions.

- can instead use the `$and` keyword and provide an array of key:value pairs.
- These two commands are equivalent:

- `db.docs.find(age:{$gt:30}, salary:{$lt:30000})`
- `db.docs.find($and:[{age:{$gt:30}}, {salary:{$lt:30000}}])`

- use the `$or` keyword to filter queries based on an OR condition.
- `$or` joins each clause with a logical OR so the query selects documents in the collection that match at least one condition.

- `db.docs.find($or:[{key1:value1}{key2:value2}])`

- `db.docs.find({ $or: [ { status: "A" }, { qty: { $lt: 30 } } ] })` to retrieve all documents in the docs collection where the status equals "A" or qty is less than ($lt) 30. (`SELECT * FROM docs WHERE status = "A" OR qty < 30`)

- AND and OR can be used together:

- `db.inventory.find( {status: "A", $or: [ { qty: { $lt: 30 } }, { item: /^p/ } })`  is the equivalent to `SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")` in SQL.

- logical NOT: can also use the `$not` to select documents that do not match the expression provided.

- `db.docs.find( {age: { $not: { $lt: 20 } } } )` to find documents where age attribute is not less than 20. This returns documents where the age field exists and is not less than 20

- logical NOR: `$nor` to select the documents that fail all the query expressions in the array.
- `db.docs.find( { $nor: [ { price: 2.00 }, { qty: { $lt: 20 }}] } )` to select all documents where the price is not 2.00 and qty field is not less than 20 and includes documents that don't contain those fields.

- can use `$nor` with `$exists` operator to only return the documents where the fields actually exist.


### The projection parameter
- The projection determines which fields are returned in the matching documents and is also an optional parameter. 
- The projection is the set set of `{}` provided to the `find` method.
- to return only the email attribute of documents where the age is greater than 18 you supply two parameters to the find method. 


`db.docs.find({age: {$gt: 20}}, {email:1})`

Here `{age: {$gt: 20}}` is the query, `{email:1}` is the projection.

- The `_id` field is always returned unless you specify not to.

- `db.docs.find({}, {_id:false, first_name:1, surname:1})`

- use `0` or `false` to not return a field
- use `1` to return a field


`db.docs.find({}, {_id:false, first_name:1, surname:1})`



## Query Examples: 


- `db.docs.find({Sex:"Male"})` to find all males in the collection, where males are identified by the attribute sex.

- `db.docs .find({Sex:"Male",Age:{$exists:true}})` to find all males that have an age attribute specified.

- `db.docs.find({$and:[{Sex:"Male"},{Age: {$exists:true}}]}`  is the same

- `db.docs.find({$or:[{Sex:"Female"},{$and:[{Sex:"Male"},{isStudent:true}]}]})` to find all male and female students



- `db.docs.find({age:22})` to find only documents where age is 22 use 
- To find only documents where age is 22 and _id is 1:
	* `db.docs.find({age:22, _id:1})`
	* `db.docs.find({$and: [{age:22}, {_id:1}]})`

- To find only documents where age is 22 or 30 
	* `db.docs.find({$or: [{age:22}, {age:30}]})` using the `$or` operator
- `$in` to finds any documents in the collection with the specified values provided in an array.
	* `db.docs.find({age: {$in: [22, 30]}})` 
- To find only documents that have a twitter attribute 
	* `db.docs.find({twitter: {$exists:true}})`
- To find only documents that have a twitter attribute and age is greater than 20
	* `db.docs.find({$and: [{twitter: {$exists: true}}, {age: {$gt: 20}}]})`

- `db.docs.findOne({twitter: {$exists: true}})` to find only one document that has a twitter attribute.

- `db.docs.findOne({carReg:{$exists:true}})` finds the first document in the docs collection which has a carReg attribute.

- `db.docs.find({}, {_id:false, name:1, surname:1})` to find all documents in the docs collection but only displat the name and surname fields.

- `db.docs.find( { status: { $in: [ "A", "D" ] } } )` to find documents with a stattus attribute of "A" or "D"

- `db.docs.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )`
 retrieves all documents in the collection where the status equals "A" or qty is less than ($lt) 30 and corresponds to the following SQL:

## Sort query results

- use the `sort()` method with the `find()` method.
- `db.docs.find({twitter: {$exists: true}}).sort({surname:1 , age:-1})` to sort all documents that have a twitter attribute alphabetically by surname and within surname, from oldest to youngest 
- **1** for **ascending** order, 
- **-1** for **descending** order.

## Limit Query results

- the `limit()` method can be used to limit the number of documents returned.

- `db.docs.find().limit(5)`

- the `skip()` method is used to skip the number of documents

- `db.docs.find({}).skip(5)` to skip the first 5 documents


***
# Update documents: `update()`

- The `save()` method replaces the existing document with the new document passed in.
- The `update()` method is used to modify existing document(s) in a collection.
- **update(query, update, options)**

- The query parameter is the first parameter passes to `update`.

- The `$set` operator is used to replace the value of a field with the set parameter. If the field does not already exist then it will add new fields with the specified values.

-  Without using the `$set` operator, the `update` command will just replace any existing attributes with the new attributes in the update command. 

- the first  `{}` to update contain the query to find the particular document to update.

- Only a single document is updated by default.

- To update an attribute for all documents in the collection can use the `update()` command and set **`multi:true`** which is the same as using the **`updateMany()`** command.

- `db.docs.update({},{$inc:{age:1}},{multi:true})` to increase all age attributes by 1. If an age attribute does not exist for a document it will add an age attribute to the document.

- `multi` can be set to true to update all documents. By default it is set to false.

- `updateMany()` does the same thing as `update()` with `multi:true`

- See also [db.collection.findOneAndUpdate](https://docs.mongodb.com/manual/reference/method/db.collection.findOneAndUpdate/#db.collection.findOneAndUpdate) method which updates a single document based on the filter and sort criteria.

- [updateMany()](https://docs.mongodb.com/manual/reference/method/db.collection.updateMany/#db.collection.updateMany) for updating all documents that match the specified filter for a collection.

- See [update operators](https://docs.mongodb.com/manual/reference/operator/update/#update-operators) on MongodB document for list of update operators including: 

- `$set` to set the value of a field in a document
- `$unset` to remove the specified fields from a document
- `$inc` Increments the value of the field by the specified amount.
- `$rename` to rename a field
- `$mul` to multiply the value of a field by a specified amount
- `$min` to only update a field if the specified value is less than the existing value
- `$max`  to only update a field if the specified value is greater than the existing value of the field.

### Some `update()` examples: 

- `db.docs.update({_id:1}, {carReg:"10-G-9876"})` would replace the entire document with _id of 1 with {carReg:"10-G-9876"}

- `db.docs.update({_id:1},{$set:{carReg:"191-K-4"}})` using the `$set` operator would update the document with the new attribute and not overwrite the other attributes. 

- `db.docs.update( {$or: [{name:"Tom"}, {name:"Mary"}]}, {$set:{address: "Galway"}}, {multi:true})`

- `db.docs.update( {experience: {$gt:20}}, {$set: {title:"Manager"}}, {multi:true, upsert:true})`

- `db.docs.save({_id:"O477", Name:"Billy",Age:29, email:"billy477@gmail.com"})` to add a new document.

- `db.people.update({_id:"O477"},{$set:{twitter:"@billy477"}})` to find the document with this id and update or add a new attribute.

- `db.docs.update({_id:106}, {$set:{fname:"Sean",Surname:"Byrne",age:33,email:"seanb1@yahoo.com"}}` to update several attributes at the same time

- `db.docs.update({},{$inc:{age:1}})` only update the first age in the first document.

- `db.docs.update({age:{$exists:true}},{$inc:{age:1}},{multi:true})` would update all age attributes by 1. if the field does not exist in a document, it will add the attribute to the document.

- `db.docs.update({},{$max:{age:31}},{multi:true})` would update the age attribute to 31 if the existing value is less than 31

- `db.docs.updateMany({_id:{$in:[101,102,103,105,106,107]}},{$set:{sex:"M"}})` would update any of the documents matching the _id attribute provided in the array provided to the `$in` operator.

- `db.docs.updateMany({sex:{$ne:"M"}},{$set:{sex:"F"}})` would update the sex attribute to "M" where it was not already equal to "M". 

- `db.docs.updateMany({$and:[{sex:"M"},{age:{$gt:20}}]},{$set:{title:"Mr. "}})` to add a new title attribute with the value Mr., to each document where the sex is M, and the age is greater than 20.

- `db.docs.updateMany({},{$rename:{fname:"Name"}})` `$rename` to rename the fname attribute to Name.

- `db.docs.update({$or:[{_id:101},{_id:103},{_id:107}]},{$unset:{carReg:""}},{multi:true})`  will remove the carReg attribute from the documents with either of these _id's.

- `db.docs.update({},{$unset:{days:""}},{multi:true})`
*** 

# Delete documents

- `deleteOne()` removes a single document from a collection that matches the filter.
- `deleteMany()` removes all documents that match the filter from a collection.

- See [db.collection.remove()](https://docs.mongodb.com/manual/reference/method/db.collection.remove/#db-collection-remove) method to remove a document from a collection which takes a query document and an option `justOne` boolean

- `db.collection.remove(<query>,<justOne>)`
- To limit the removal to just one document, set the optional `justOne` parameter to `true`. (default valus is `false`.)

- `db.docs.remove( { } )` will remove all documents from the docs collection
- `db.docs.remove( { qty: { $gt: 20 } } )` to remove all documents where the qty field is greater than 20


***
# Indexes

- By default the only index on a document is on the _id field.

- To find the indexes on a collection: `db.Collection.getIndexes()`
- Which returns information in the following format, detailing the index field (_id) and the order of the indexes (1 is ascending; -1 is descending:

```
"key" : {
	"_id" : 1
},
```

- `db.collection.createIndex()` to create an index on a field other than _id: 

-  `db.collection.dropIndex()` to drop an index on a field.
- `db.docs.createIndex({age: 1})` creates an index on the age field
-  `db.docs.dropIndex({age: 1})` to drop the index on the age field .
- NOTE: The index on _id cannot be dropped


***
# Relationships in MongoDB
Relationships represent how documents might be related to other documents.

- One-to-One Relationships with Embedded Documents
- One-to-Many Relationships with Embedded Documents
- One-to-Many Relationships with Document References

## One-to-One Relationships with Embedded Documents

Documents can be **embedded** inside another document. This can be used to keep all related data inside a single document making the data easy to retrieve. An attribute in a document can contain a document.

An example use would be a document for a person that contains a document containing address details.

- When querying embedded documents use dot notation and quotes.

- `db.docs.find({address:{$exists:true}})`
>{ "_id" : "x1234", "name" : "John Smith", "address" : { "_id" : 101, "town" : "Ballybunion", "county" : "Kerry" } }  
>{ "_id" : "x1235", "name" : "Jane Sweets", "address" : { "_id" : 102, "town" : "Clane", "county" : "Kildare" } }

- `db.docs.find({address:{$exists:true}},{_id:0,"address.town":1})`

>{ "address" : { "town" : "Ballybunion" } }  
> { "address" : { "town" : "Clane" } }



Here the document below contains an embedded document in the `engine` attribute.
>` "{_id" : "11-G-987", "make" : "Ford", "model" : "Mondeo", "engine" : { "size" : 1.6, "zeroToSixty" : 8, "bhp" : 120 } }`

- `db.docs.find({"engine.bhp":{$gt:115}})` where `bhp` is a sub-document of (or contained within) the `engine` document so use `"engine.bhp"`, `"engine.size"` etc to access these attributes.

- `db.docs.find({"engine.bhp":{$gt:115}},{make:true, model:true,_id:true})`


### One-to-Many Relationships with Embedded Documents

One document can be associated with many documents. For example one student may take several modules.
An array is an ordered collection of data. This can contain the many relationships.

The following documents each contain an embedded "modules" document that contains several name : value pairs for each module taken.

> { "_id" : "G00101224", "name" : "Mary", "modules" : [ { "_id" : "M100", "module" : "Databases" }, { "_id" : "M101", "module" : "Java" } ] }

>{ "_id" : "G00101226", "name" : "Emer", "modules" : [ { "_id" : "M100", "module" : "Databases" }, { "_id" : "M104", "module" : "Python" } ] }  

>{ "_id" : "G00101229", "name" : "Sam", "modules" : [ { "_id" : "M104", "module" : "Python" }, { "_id" : "M101", "module" : "Java" } ] }

The following query will return the modules for each student:
`db.student.find({},{"modules.module":1}`

>{ "_id" : "G00101224", "modules" : [ { "module" : "Databases" }, { "module" : "Java" } ] }
{ "_id" : "G00101226", "modules" : [ { "module" : "Databases" }, { "module" : "Python" } ] }
{ "_id" : "G00101229", "modules" : [ { "module" : "Python" }, { "module" : "Java" } ] }

## One-to-Many Relationships with Document References

- Using document references is a way of normalising relationships between documents. In this way, documents can be maintained separately with the document containing a field that references the id of another document.


This is the approach of designing normalized relationship. In this approach, both the user and address documents will be maintained separately but the user document will contain a field that will reference the address document's id field.

Here the module field in the a document is an array where the values stored in the array correspond to `_id` field in a `module` document.

- The aggregation pipeline stage `$lookup` is used to get information from documents with document references and can be thought of as similar to a `join` in SQL.

- The [$lookup (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/) pipeline stage performs a left outer join to an unsharded collection in the same database to filter in documents from the “joined” collection for processing. 
- `$lookup` performs an equality match between a field from the input documents (localField) with a field from the documents of the joined collection (foreignField). 

- `$lookup` takes 4 fields, 
	* `from` is the collection in which to perform the lookup
	*  `localField` - the field from the input document being searched for
	* `foreignField` - the field from the documents of the from collection, the field to search for the `localField` value(s) in 
	* `as` is any string provided as the name for the output array field. 


- `db.docs.aggregate([{$lookup:{from:"docs" ,localField:"author", foreignField:"_id",as:"Written by"}}])` *Show the details of all books and for each book also show all details of the corresponding author as "Written by". Sort the results by authors name.*



### examples

- `db.docs.aggregate([{$match: {name:"Tom"}},{$lookup: {from:"docs",localField:"addresses",foreignField:"_id", as:"Lived In"}}])` to show all details for “Tom” including full details of his addresses

- `db.docs.aggregate([{$lookup:{from:"docs" ,localField:"author", foreignField:"_id",as:"Written by"}}])` to show the details of all books and for each book also show all details of the corresponding author as "Written by". 

>{ "_id" : "2", "name" : "Bill", "addresses" : [ "01001", "12967", "32920" ] }








***
# Aggregation

- Aggregation operations are used to return computed results from documents.
- Values from multiple documents are grouped together and operations are performed on the grouped data to return a single result. 
- **aggregate()** calculates aggregate values for the data in a collection such as min, max, average etc.

The `aggregate()` method takes 2 parameters:
- `db.collection.aggregate(pipeline, options)`
- The **pipeline stages** parameter is an array of options or **stages**, 
- The **pipeline operators** which is an optional parameter and can be used to change the way the aggregation method works.

The concept of a pipeline is similar to that in UNIX where the output of one operation is used as the input for another operation.

- In the `db.collection.aggregate` method, pipeline stages appear in an array. Documents pass through the stages in sequence. Most stages can appear more than once in a pipeline.

- The [db.collection.aggregate(pipeline, options)](https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#definition) method calculates aggregate values for the data in a collection or a view. 
- The pipeline parameter takes an array containing a sequence of data [aggregation operations or stages](https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/). The `options` optional parameter takes a document containing additional options.


## `aggregate()` method

- The `aggregate()` method takes a pipeline stages parameter which is an array `[]`. 
-  `db.collection.aggregate( [ { <stage> }, ... ] )`
- **When using `aggregate()` method you must use a `$` in front of the field.** Using the `db.collection.aggregate` method, pipeline stages appear in an array. 


## Aggregation pipeline stages include:

-  `$count` : to return a count of the number of documents at this stage of the aggregation pipeline
-  `$group` : to group input documents by a specified identifier expression and applies the accumulator expression(s), if specified, to each group.
- `$bucket` : to categorise incoming documents into groups, called buckets, based on a specified expression and bucket boundaries.
-  `$lookup`: Performs a left outer join to another collection in the same database to filter in documents from the “joined” collection for processing.
-  `$match`: Filters the document stream to allow only matching documents to pass unmodified into the next pipeline stage. 
- `$merge`: to write the resulting documents of the aggregation pipeline to a collection
- `$project`: Reshapes each document in the stream, such as by adding new fields or removing existing fields. For each input document, outputs one document. (See `$set` and `$unset` which are aliases for `$project`)
- `$set` : to add new fields to the document
- `$unset`: to remove or exclude fields from documents. 
- `$sort`: to sort the document stream by a specified sort key. 
and more. 

- **Groups** input documents by the specified `_id` expression and for each distinct grouping, outputs a document. 
- The `_id` field of each output document contains the unique group by value. 
- The output documents can also contain computed fields that hold the values of some **accumulator expression**.

[$group (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group)

**$group**:
- `$group` is an aggregation pipeline *stages*. It works the same as `group by` in MySQL. 
- The value of `$group` is a document. 
- `_id` is mandatory and is the documents you wish to group by.
- can set the `_id` to **null** so as not to aggregate by any particular ids.
- `field1` is optional and computed using **accumulator operators**. 
- Both `_id` and the accumulators accept expressions.

The $group **stage** has the following prototype form:

```json
{
  $group:
    {
      _id: <expression>, // Group By Expression
      <field1>: { <accumulator1> : <expression1> },
      ...
    }
 }
 ```

### Accumulator Operators:
Accumulator operators include `$avg` for averages, `$min`, `$max`, `$sum`, `$first` and `$last`

- [{ $sum: <expression> }](https://docs.mongodb.com/manual/reference/operator/aggregation/sum/)

- the results of the aggregate method can be sorted by using the `sort` pipeline stage.





## Aggregation examples using the `group` pipeline stage

- `db.docs.aggregate([{$group : {_id: null, Average: {$avg: "$gpa"}}}])` to get the average gpa for all student `_id: null` where 'Average' is the string to return the results as. 'gpa' is the attribute to get the average of.

- `db.docs.aggregate([{$group : {_id:"$age", "Max GPA per Age": {$max: "$gpa"}}}]` gets the maximum gpa per age group and returns it as 'Max GPA per Age'.)

- `db.docs.aggregate([{$group : {_id:"$age", "Max GPA per Age":{$max:"$gpa"}}},{$sort:{_id:1}}])`

- `db.docs.aggregate([{$group:{_id:null, "Total Age":{$sum:"$age"}}}])` to show the combined ages of everyone in the collection as "Total Age".

- `db.docs.aggregate([{$group:{_id:"$sex", "Total Age":{$sum:"$age"}}}])` to get the total age by sex.  Note that documents with a value of `null` for the sex attribute will not be included.

- `db.docs.aggregate([{$group:{_id:"$model","Avg BHP":{$avg:"$engine.bhp"}}}])` to show the average bhp for each model of car.











