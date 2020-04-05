# MongoDB

- [MongoDB](https://docs.mongodb.com/manual/introduction/) is a document database designed for ease of development and scaling. 
It is used for very large databases and also in areas where the data is much less structured than in traditional relational database environments.
MongoDB is based on JSON  and has the same concept as databases in relational databases.

A record in MongoDB is a document, which is a data structure composed of field and value pairs. MongoDB documents are similar to JSON objects. The values of fields may include other documents, arrays, and arrays of documents. (like a row in a relational database)

MongoDB stores documents in collections. A **collection** is a set of related documents which can be thought of as a table in a relational database.



## Installing MongoDB

See [Installing MongoDB on Mac (Catalina)](https://zellwk.com/blog/install-mongodb/) in relation to changes due to Catalina updates. Also [Install mongoBD on os-x](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/) and [download mongoDB](https://www.mongodb.com/download-center/community).

- Select latest version for macOS x64 to download. 
- Can downloaded a .tgz tarball or install on mac using the homebrew package manager.
 
I followed the instructions at[installation manual](https://docs.mongodb.com/manual/installation/). It is recommended not to install it using the tarball and instead using the homebrew package manager.

According to [Installation Method](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x-tarball/),while MongoDB can be installed manually via a downloaded .tgz tarball as described in this document, it is recommended to use the `brew` package manager on your system to install MongoDB if possible. Using a package manager automatically installs all needed dependencies, provides an example mongod.conf file to get you started, and simplifies future upgrade and maintenance tasks.

See the [tutorial: install mongoDB on os-x](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

- Installed XCode.
- `brew tap mongodb/brew`

Installed MongoDB Community Edition using the third-party brew package manager.
In terminal `brew install mongodb-community@4.2`

To run mongodb `brew services start mongodb-community@4.2`

To begin using MongoDB, connect a mongo shell to the running instance. From a new terminal, issue the following: `mongo`. See [Connect and Use MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/#connect-and-use-mongodb)

See [mongo installation](https://treehouse.github.io/installation-guides/mac/mongo-mac.html)

(base) `$ brew services start mongodb-community`
>Service `mongodb-community` already started, use `brew services restart mongodb-community` to restart.
(base) $ `brew services restart mongodb-community`
Stopping `mongodb-community`... (might take a while)
==> Successfully stopped `mongodb-community` (label: homebrew.mxcl.mongodb-commu
==> Successfully started `mongodb-community` (label: homebrew.mxcl.mongodb-commu

To verify that MongoDB is running, search for mongod in your running processes:
(base) $ `ps aux | grep -v grep | grep mongod`
angela    90664   0.0  0.5  5526108  40668   ??  S     8:27pm   0:01.29 /usr/local/opt/mongodb-community/bin/mongod --config /usr/local/etc/mongod.conf
(base) A's-MacBook-Pro:bin angelacorkery$ 

***
if MongoDB is installed, to run type the command `mongod` into the Terminal.
This starts mongoDB in the background.

***

## Why NoSQL databases? 

Relational databases were designed to run on a single server. Servers resources can be overextended if the data gets beyond a certain size.
- Scale up vertically (bigger server etc)
- Scalability
- Scale out horizontally (split the databases across many servers is problematic for example if tables were spread across different servers).

Scaling horizontally or vertically is not a good solution for relational databases as they are not designed for th amount of data being generated these days.

When relational databases are designed, the schema is set up beforehand. It is not easy to change the schema especially when scaling up or out. In a relational model, we need to store the same information for each record (or null). Also in an agile software development where changes are created in a series of iterations, this constant change does not work well with relational databases. NoSQL databases were created to overcome these type of problems.

MongoDB provides horizontal scalability as part of its core functionality. Sharding distributes data across a cluster of machines.


### Document Database
MongoDB is a popular such document database.
In a document database, each record and it's associated data is thought of as a document. Each document is usually stored together, unlike relational dbs where information is stored over several tables and are joine dtogether in queries.

### Schemaless
There is no schema in a nosql database. Each document can store whatever is applicable to it.

### Horizontal Scalability through Sharding
      
Sharding sperates large databases into smaller, more easily managed databases called shards
In sql, sharding is a complex process but it is easily faciliated in mongodb.

### Duplication of data
Duplication of data might seem wasteful but all the data for a single document is stored in that docment and no need to join to another doc to get mnore informatiomn.

# JSON

- JSON – JavaScript Object Notation
- Lightweight data-interchange format 
- Machine/Human readable
- Language independent
- JSON Structure:
	* Name/Value pairs
	* Ordered Lists

"name" : "value" pairs are separated by a colon `:`

## JSON Datatypes

### Numbers
Unlike other languages, you don't have to declare a number as an integer or float etc.
`{"id" : 1}`

### Strings
Strings are surrounded by quotes. `{"fname": "John"}`

### Booleans

`{"name": false}`

### Array

Arrays are ordered collecion of data.
`{"subjects" :["Databases","Web App", "CTA"]}`


**Objects can be stored in other objects.**
```json
{
"student":"G00257854",
 "address":{
	"street":"Castle St", 
	"town":"Athenry", 
	"county":"Galway"
} }
```
See [newsapi](https://newsapi.org) for example of JSON code.


## JSON uses.
JSON is widely used to publish information on the internet. An application can connect to a site and combine data from other sites to give new interesting information.

JSON is a widely used format for data exchange, especially on the internet. 
In Mongodb, a document is basically a JSON object but they are stored as BSON objects

## MongoDB, JSON and BSON
- JSON object = MongoDB document
- Internally, MongoDB represents JSON documents in binary-encoded format called BSON (Binary javaScript Object Notation) (binary JSON)
- BSON extends the JSON model to provide additional data types (such as date) as well as indexes.
***
# MongoDB structures

### Document
- A **document** is a record in a MongoDB collection and the basic unit of data in MongoDB.
- Documents are analogous to JSON objects or records in an relational database

```json
{
"_id" : ObjectId("5919fecf0822ef8ecec132f8"),
"name" : "John",
"house" : 31,
"street" : "Main St.",
"town" : "Athenry"

```

### Collection

MongoDB stores documents in collections (which are analogous to tables in relational databases). If a collection does not exist, MongoDB creates the collection when you first store data for that collection.

- A **collection** is a grouping of MongoDB documents.
- Collections are analogous to relational database tables.
- A collection exists within a single database.
- Collections do not enforce a schema. Documents within a collection can have different fields.
- Typically, all documents in a collection have a similar or related purpose.

### Database

- A number of **databases** can be run on a single MongoDB server.
      
- `show dbs` Show databases
- `use <db>` Switch to a database if it exists. If it does't already exist, Mongo creates it.
- `db` to show current database (like select database)
- `show collections` to show collections in the current database (like show tables)

## Using MongoDB

- `db` to show the current database
- `use <db name>` to switch databases
- `db.collection.save()` to save a document to a collection (or create the collection if it doesn't aready exist.)
- `db.collection.insertMany()` to insert multiple documents into a collection
- `db.collection.find({})`  to select all documents in a collection
- `db.collection.find({}).pretty()` to format the results 
- `db.collection.find({<name>:<value>})` to filter the query documents using equality matches.
- [`db.collection.find(query, projection)`](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find) to specify the fields to return.


`db.collection.find({})` is like `SELECT * FROM collection` in MySQL
`db.collection.find({status:"D"})` is like `SELECT * FROM inventory WHERE status = "D"`




***
## MongoDB Rules for creating a document.

- a document must have an `_id` field. If one isn't provided, then it is automatically generated.

- The `_id` cannot be an array.


## Create a document - `save()`

A MongoDB document is analagous to a JSON object and therefore consists of name:value pairs separated by : and surrounded by curly braces {}.
To create a document, first call the `db.save` method and pass an argument to the method which is the document to save. State the name of the collection being saved to (User in the example below).

Saving a document to a collection is analagous to inserting a record into a relation. You must also state which database to save to. Note that `db` is not the name of the database but a reference to the current database.

```json
db.User.save( 
{ 	_id:1,
	first_name : "John", 
	surname : "Smith", 
	email : "john@gmail.com"
})
```

See [`db.collection.insertMany()`](https://docs.mongodb.com/manual/reference/method/db.collection.insertMany/#db.collection.insertMany) for inserting multiple documents into a collection.
## Query the Database - `db.collection.find()` method

- Use the `db.collection.find()` method to select the documents from a collection. 
- To select all documents in the collection, pass an empty document as the Query Filter document to the method.
- Use query filter documents to specify the conditions that determine which records to select 

`db.User.find()` where db refers to the current database ("MyDB"), `User` is the name of the collection to find the documents in. `find` is the name of the method.

The `find` method finds data in a collection. If no parameters are passed (or an empty document) then all documents in the collection will be returned. Also need to state which collection and which database to find the document in.
`db.User.find().pretty()` 

The `.pretty()` method can be appended to the `find()` method to format the results. It spaces out name value pairs to make them easier to read by humans. 

The number of documents returned by a `find` can be limited by providing a query to it. The query filter document is like a smaller document.
An equality match is specified as `{<field>:<value>}` to filter the results.
(Equality matches on the embedded document require an exact match, including the field order.)

For an equality match (i.e. <field> equals <value>), specify <field>: <value> in the query filter document and pass to the db.collection.find() method.

##### $and: operator, $or operator etc
These operators can be used to narrow down the results to be more specific. 
Provide an array of name:value pairs to the `$and` and `$or` operators.
Provide an array of values to the `$in` operator.
MongoDB does not have a schema. Some attributes might be common to all documents (which is why they are in the same collection) but other attributes will be in some documents and not others. The `$exists` operator can be used to find documents with specific attributes.

Can find documents with specific attributes using $exist operators

For example.
- To find only documents where age is 22 use `db.User.find({age:22})`
- To find only documents where age is 22 and _id is 1:
	* `db.User.find({age:22, _id:1})`
	* `db.User.find({$and: [{age:22}, {_id:1}]})`

- To find only documents where age is 22 or 30 
	* `db.User.find({$or: [{age:22}, {age:30}]})` using the `$or` operator
	using the `$in` operator. $in finds any documents with the specified values provided in an array.
	* `db.User.find({age: {$in: [22, 30]}})` using the `$in` operator

- To find only documents that have a twitter attribute 
	* `db.User.find({twitter: {$exists:true}})`
- To find only documents that have a twitter attribute and age is greater than 20
	* `db.User.find({$and: [{twitter: {$exists: true}}, {age: {$gt: 20}}]})`

### Query the Database - findOne()

Queries can become increasingly complex just like with relational databases.
To find only one document that has a twitter attribute use `db.User.findOne({twitter: {$exists: true}})`. 
Note that the `findOne` method returned only one document that matches. The document returned is the first document and depends on the order of the documents in the database and this could change from query to query.

### Query the Database - sort()

Can use the `sort()` method with the `find()` method.

For example to sort all documents that have a twitter attribute alphabetically by surname and within surname, from oldest to youngest `db.User.find({twitter: {$exists: true}}).sort({surname:1 , age:-1})`

**1** for **ascending** order, **-1** for **descending** order.`

## MongoDB - _id

- The document ID (_id) attribute of a MongoDB document is the only mandatory part of a document.
- The document ID can be any value, except an array.

###  save()

If you pass a document id to the `save` method where the id already exists, it overwrites the existing document. The `save` method calls one of two method `insert` or `update`. Save is a **wrapper method** whose main purpose is to call another method. Wrappers in programming are used to hide or abstract details.

### insert()

- Inserts a document or documents into a collection.

To insert multiple documents, pass them to the insert method in an array. An array is an ordered collection of data in square brackets. The attributes of each document do not have to be the same.

### update()

- Modifies an existing document or documents in a collection.
- **update(query, update, options)**

The first parameter passed to the update method is the query.

The `$set` operator is used to replace the value of a field with the set parameter. If the field does not already exist then it will add new fields with the specified values.

`multi` can be set to true to update all documents. By default it is set to false.

`db.mydoc.update( {$or: [{name:"Tom"}, {name:"Mary"}]}, {$set:{address: "Galway"}}, {multi:true})`

`db.mydoc.update( {experience: {$gt:20}}, {$set: {title:"Manager"}}, {multi:true, upsert:true})`

### deleteOne()

- removes a single document from a collection.
Removes a single document that matches the filter. (The filter is just a query.)

### deleteMany()
- Removes all documents that match the filter from a collection. 


 ## Operators      

- [All operators](https://docs.mongodb.com/manual/reference/operator/)

- [Update operators](https://docs.mongodb.com/manual/reference/operator/update/%23id1)

- [Logical Query Operators](https://docs.mongodb.com/manual/reference/operator/query-logical/)

- [Comparison Query Operators](https://docs.mongodb.com/manual/reference/operator/query-comparison/)


***


1. Create a mongodb database called peopleDB
Add the following people

`use peopledB`
if it doesn't already exist, mongodb will create the database.
`db` always refers to the current database. This command will return the current db.
>peopleDB

`db.people.save()`

Pass in an attribute or parameter - an object starts and ends with a curly brace.
Can use quotes but don't have to here as it can get hard to read with all the brackets, curly braces etc.passing in the id attribute, then the name attribute

pass  in an object or document.
`db.people.save({_id:"G103", Name:"John", Age:23, Sex:"Male",isStudent:true})`

We don't have to create any collection, once we specify a collection, if it doesn't already exist it will be created. 

`db.people.find()`

add another person

`db.people.save({_id:"D313", Name:"Molly",Age:24})`

Here we are not entering the same amount of information. Adding less attributes. MongoDB is schemeless so every document does not have to have the same type of attributes, unlike in a relational database such as MySQL.
Some documents have the same fields, while others won't.
The schemeless nature of mongodb. Every document doesn't have to have the same attributes. It is a collection of related data and may have different characteristics.

`db.people.save({_id:"M234", Name:"Ray", Sex:"Male", isStudent:true})`
`db.people.save({_id:"M223", Name:"Tom", Age: 24, Sex:"Male", isStudent:false})`

`db.people.find()`

{ "_id" : "G103", "Name" : "John", "Age" : 23, "Sex" : "Male", "isStudent" : true }
{ "_id" : "D313", "Name" : "Molly", "Age" : 24 }
{ "_id" : "M234", "Name" : "Ray", "Sex" : "Male", "isStudent" : true }
{ "_id" : "M223", "Name" : "Tom", "Age" : 24, "Sex" : "Male", "isStudent" : false }
{ "_id" : "W989", "Name" : "Mary", "Age" : 25, "Sex" : "Female" }


`db.people.find().pretty()`

{
	"_id" : "G103",
	"Name" : "John",
	"Age" : 23,
	"Sex" : "Male",
	"isStudent" : true
}
{ "_id" : "D313", "Name" : "Molly", "Age" : 24 }
{ "_id" : "M234", "Name" : "Ray", "Sex" : "Male", "isStudent" : true }
{
	"_id" : "M223",
	"Name" : "Tom",
	"Age" : 24,
	"Sex" : "Male",
	"isStudent" : false
}
{ "_id" : "W989", "Name" : "Mary", "Age" : 25, "Sex" : "Female" }


Show all males.

run on the peoples collection.

See [db.collection.find()](https://docs.mongodb.com/manual/reference/method/db.collection.find/index.html).

Want to find all males in the collection, where males are identified by the attribute sex.

 `db.people.find({Sex:"Male"})`
{ "_id" : "G103", "Name" : "John", "Age" : 23, "Sex" : "Male", "isStudent" : true }
{ "_id" : "M234", "Name" : "Ray", "Sex" : "Male", "isStudent" : true }
{ "_id" : "M223", "Name" : "Tom", "Age" : 24, "Sex" : "Male", "isStudent" : false }

Show all males that have an age attribute specified.

[exists](https://docs.mongodb.com/manual/reference/operator/query/exists/index.html)

db.people.find({Sex:"Male",Age:{$exists:true}})
{ "_id" : "G103", "Name" : "John", "Age" : 23, "Sex" : "Male", "isStudent" : true }
{ "_id" : "M223", "Name" : "Tom", "Age" : 24, "Sex" : "Male", "isStudent" : false }

Could use an editor such as notepad ++ or this I guess which supports JSON. Write the code in the editor as it will prompt the closing brackets.
db.people.find({ Age: { $exists: true}})

db.people.find({$and: [{Sex:"Male"},{Age:{$exists: true}}]})


the values here are in an array [].
```json
db.people.find({$and:[{Sex:"Male"},{Age: {$exists:true}}]})
```

{ "_id" : "G103", "Name" : "John", "Age" : 23, "Sex" : "Male", "isStudent" : true }
{ "_id" : "M223", "Name" : "Tom", "Age" : 24, "Sex" : "Male", "isStudent" : false }

Show all male students and all females.

This means only males that are students and all females.

Everything is a `name:value`, an `$or;`  or `$and;` takes an array []

```json
db.people.find({$or:[{Sex:"Female"}]})
``` 
> { "_id" : "W989", "Name" : "Mary", "Age" : 25, "Sex" : "Female" }


### Ands and ORs together


Show all male students and all females.

```json
db.people.find({$or:[{Sex:"Female"},{$and:[{Sex:"Male"},{isStudent:true}]}]})

```

Add a new document to the people collection.

_id O477, Name Billy, Age 29, email, Billy477@gmail.com

```json
db.people.save({_id:"O477", Name:"Billy",Age:29, email:"billy477@gmail.com"})
```

Add the following attribute to the document just updated.
twitter: @billy477

update will apply to the document with the id attribute O477. Need to use the $set operator otherwise the update command will replace the existing attributes with the new attributes. If the field being added does not already exist, set will 

the first part of the update is the query part (finding the document with the particular id). The second part of the update is $set:value
```json
db.people.update({_id:"O477"},{$set:{twitter:"@billy477"}})

```
This finds the document with the id and adds a new attribute for the twitter field.


 db.people.find()
{ "_id" : "G103", "Name" : "John", "Age" : 23, "Sex" : "Male", "isStudent" : true }
{ "_id" : "D313", "Name" : "Molly", "Age" : 24 }
{ "_id" : "M234", "Name" : "Ray", "Sex" : "Male", "isStudent" : true }
{ "_id" : "M223", "Name" : "Tom", "Age" : 24, "Sex" : "Male", "isStudent" : false }
{ "_id" : "W989", "Name" : "Mary", "Age" : 25, "Sex" : "Female" }
{ "_id" : "O477", "Name" : "Billy", "Age" : 29, "email" : "billy477@gmail.com", "twitter" : "@billy477" }



Increase peoples age (where appropriate) by 1.

Will only want to increase age where an age exists. 

[Increments  $inc:](https://docs.mongodb.com/manual/reference/operator/update/inc/index.html)
The $inc operator increments a field by a specified value and has the following form.
`{ $inc: { <field1>: <amount1>, <field2>: <amount2>, ... } }`

```json

db.people.find({Age:{$exists:true}})
db.people.update({Age:{$exists:true}},{$inc:{Age:1}},{multi:true})
```

update by default only runs on the first document that matches the query. Can specify the third parameter to update which is the options.

[update](https://docs.mongodb.com/manual/reference/command/update/index.html)
multi: Optional. If true, updates all documents that meet the query criteria. If false, limit the update to one document that meet the query criteria. Defaults to false.

### To start using Mongo: 

Enter the command `$ mongo` in the terminal

### To quit from mongo
To quit, `quit()` to exit mongo.

*** 

### To import a database

The `mongo import.exe` program is located in program files or wherever it is installed in your system. In a mac if `brew` was used to install mongodb then `mongod` is located in `/usr/local/bin/`.
See [stackoverflow - where is monogimport installed on a mac](https://stackoverflow.com/questions/25850467/where-is-mongoimport-installed-on-mac-os-x)
    

--db mydemo --collection docs --file (the file name)


/Users/ang../downloads/demo1.json

`--db mydemo --collection docs --file /Users/ang.../downloads/demo1.json`

mongoimport --db=mydemo --collection=docs --file=/Users/ang.../downloads/demo1.json


## db.collection.find(query, projection)

The syntax of the find method is `find(query, projection)` where the query is what you are looking for - whatever documents match this query is returned. The query parameter is an optional parameter. 

The projection determines which fields are returned in the matching documents and is also an optional parameter. The projection is similar to the select clause is mysql


- to return only the email attribute of documents where the age is greater than 18 you supply two parameters to the find method. 

```json
db.users.find({age: {$gt: 20}}, {email:1})
```
The `{age: {$gt: 20}}` is the query. 
The `{email:1}` is the projection.

The following command returns only the first name and surname of all documents.
The first set of {} is the query, the second set is the projection.

Note that the `_id` field is always returned unless you specify not to.

Here the query is the first parameter. {} will find all documents.
The `{_id:false, first_name:1, surname:1}` is the projection. It will only return the first name and surname attributes. It will not return the `_id` attribute as this has been set to `false`.

```json
db.users.find({}, {_id:false, first_name:1, surname:1})
```

## db.collection.aggregate(pipeline, options)

**aggregate()** calculates aggregate values for the data in a collection such as min, max, average etc.

The `aggregate()` method takes 2 parameters. 
- The **pipeline stages** parameter is an array of options or **stages**, 
- The **pipeline operators** which is an optional parameter and can be used to change the way the aggregation method works.

[db.collection.aggregate(pipeline, options)](https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#definition) calculates aggregate values for the data in a collection or a view.

- The pipeline parameter takes an array containing a sequence of data [aggregation operations or stages](https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/).

- The `options` optional parameter takes a document containing additional options.(not using any here)


[$group (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group)

- **Groups** input documents by the specified `_id` expression and for each distinct grouping, outputs a document. 
- The `_id` field of each output document contains the unique group by value. 
- The output documents can also contain computed fields that hold the values of some **accumulator expression**.

## `aggregate()` method
See [aggregation quick reference manual](https://docs.mongodb.com/manual/meta/aggregation-quick-reference/).

The `aggregate()` method calculates aggregate values for the data in a collection.
`db.collection.aggregate(pipeline, options)`

- The `aggregate` method takes one parameter which is an array `[]`. When using aggregate you must use a `$` in front of the field. Using the `db.collection.aggregate` method, pipeline stages appear in an array. 
- `db.collection.aggregate( [ { <stage> }, ... ] )`

In the `db.collection.aggregate` method, pipeline stages appear in an array. Documents pass through the stages in sequence. Most stages can appear more than once in a pipeline.

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

The `$group` stage has the following prototype form:
```
{
  $group:
    {
      _id: <expression>, // Group By Expression
      <field1>: { <accumulator1> : <expression1> },
      ...
    }
 }
 ```

### Average

- Get the Average gpa for all students:

```json
db.users.aggregate([{$group : {_id: null, Average: {$avg: "$gpa"}}}])
```
**$group**:
- `$group` is an aggregation pipeline *stages*. It works the same as `group by` in MySQL. 
- The value of $group is a document. 
- `_id` is mandatory and is the documents you wish to group by.
- can set the `_id` to **null** so as not to aggregate by any particular ids. 

- In this example Average is the string we want to return the results as. 
- `$gpa` is the attributes to get the average of. 

- This example gets the maximum gpa per age group and returns it as 'Max GPA per Age'.

- When using `aggregate` you need to put a $ dollar sign in front of the field.

```json
db.march.aggregate([{$group : {_id:"$age", "Max GPA per Age": {$max: "$gpa"}}}])

```

- `db.collection.aggregate( [ { <stage> }, ... ] )`

- [{ $sum: <expression> }](https://docs.mongodb.com/manual/reference/operator/aggregation/sum/)

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

 - `_id` is required
 - `field1` is optional and computed using **accumulator operators**. 
 - Both `_id` and the accumulators accept expressions.
 
### Accumulator Operators:

Accumulator operators include `$avg` for averages, `$min`, `$max`, `$sum`, `$first` and `$last`

### Sorting the results of aggregate()

To sort the result of the aggregate method use the `sort` pipeline stage.
```json
db.march.aggregate([{$group : {_id:"$age", "Max GPA per Age":{$max:"$gpa"}}},{$sort:{_id:1}}])
```

***
## Indexing 

Indexing is used to support the efficient execution of queries.

The following is just pseudo-code to show what is happening if looking for users where age is greater than a value. It would have to go through each document in turn looking for the matching documents which could take a long time if the collection was very large. If the documents were spread across many shards this could take a long time.

```
for each document d in ‘User’ { if (d.age == 35) {
return d; }
}
```
- Indexes support the efficient execution of queries in MongoDB.
- Without indexes, MongoDB must perform a collection scan, i.e. scan every document in a collection, to select those documents that match the query statement.
- Indexes are special data structures that store a small portion of the collection’s data set in an easy to traverse form.
- Indexes hold mappings from field values to document locations.


If we knew we would be searching for documents by age then age could be set as an index. The index stores a value for a field or a specific set of fields by the value of the fields. Then can check if the age exists in the age index table, and only then need to check the document at those specific addresses. 
Indexes save time by not doing a collection scan - by not reading every single document in the collection. However indexes should be used in moderation.
Consider what happens when writing to an index field. If adding an index for a new document with a new age value, space would need to be made in between the values below and above it. 
Then if a document was deleted, as well as deleting the document, the age index table would also need to be updated.
Having too many or too complex indexes on documents would also negatively impact on performance.


### getIndexes()

- By default the only index on a document is on the _id field.

- To find the indexes on a collection: `db.Collection.getIndexes()`
- Which returns information in the following format, detailing the index field (_id) and the order of the indexes (1 is ascending; -1 is descending:
```
"key" : {
	"_id" : 1
},
```

### createIndex()

- To create an index on a field other than _id: `db.Collection.createIndex()`

```json
db.User.createIndex({age: 1})
```

### dropIndex()

- To drop an index on a field use `db.Collection.dropIndex()`
- To drop the index on the age field (just created) use `db.User.dropIndex({age: 1})`
- NOTE: The index on _id cannot be dropped

## Sort()

- When a sort() is performed on a field that is not an index, MongoDB will sort the results in memory.

- If the sort() method consumes more than 32MB of memory, MongoDB aborts the sort and returns an error

- To avoid this error, create an index supporting the sort operation.


***

## Relationships in MongoDB

Relationships represent how documents might be related to other documents. 

### Modelling relationships between documents: 

- One-to-One Relationships with Embedded Documents
- One-to-Many Relationships with Embedded Documents
- One-to-Many Relationships with Document References

### One-to-One Relationships with Embedded Documents

Documents can be **embedded** inside another document. This can be used to keep all related data inside a single document making the data easy to retrieve.

Here the query parameter is the empty document which returns all matching documents. The projection parameter contains 3 attributes where the address attribute is an embedded document.

```json

db.student.find({},{address:1})
{ "_id" : "G00789445", 
  "address" : {
		"_id" : 100,
		"town" : "Athenry", 
		"county" : "Galway“
} }
``` 

- Show only the county field of documents that have an address field
```json
db.student.find({address:{$exists:true}},{_id:0,"address.county":1})
```

The query parameter here is the address field  `{address:{$exists:true}`  which says to only return documents where the address field exists. 
The projection parameter `{_id:0,"address.county":1}` says to not return the id field and to return the county field of the embedded address document. This is not part of the person document (which only contains id, name and address). The county field is part of the embedded address document of the address attribute. 
Embedded documents are surrounded by quotation marks `"address.county"``

{ "address" : { "county" : "Galway" } 

### One-to-Many Relationships with Embedded Documents

One document can be associated with many documents. For example one student may have several modules.
An array is an ordered collection of data. This can contain the many relationships.


```json
db.student.save({_id:"G00101226", 
				name:"Mary",
				modules: [{_id:"M100", module:"Databases"}, 
				{_id:"M101", module:"Java"}]})
```


Here a single parameter is provided to the save method with 3 name:value pairs.
id, name and modules. Modules is an array with 2 elements, each of which is a document. The first of these documents `{_id:"M100", module:"Databases"}` has 2 name:value pairs. The second document `{_id:"M101", module:"Java"}` also has two name value pairs.


- Show the student’s _id and module of all modules taken by student G00101224

```json
db.student.find({_id:"G00101224"},{"modules.module":1}
```

The `{_id:"G00101224"}` is the query to find the document with this particular id. 
The `{"modules.module":1}` is the projection to only return the id and modules.

### One-to-Many Relationships with Document References

For example have a student with embedded documents for each module taken. Then have another student with another embedded documents with each module taken. This is duplication of the data. Instead the module documents could be referenced and then only stored in the one place.

```json
db.docs.save({_id : "M100", module : "Databases" }) 
db.docs.save({_id : "M101", module : "Java" })
```
This create the modules documents in a collection called docs.

```json
db.docs.save({_id: "G00101224", name: "Mary", modules: ["M100", "M101"]}) 
db.docs.save({_id: "G00205266", name: "Sarah", modules: ["M100", "M101"]})
 
```

This creates the students documents  in the same collection.
As a student can take more than one module, the modules field is an array. The values stored in the modules array correspond to the `_id` fields in the modules document.

**To get information from documents with document references, need to use the aggregation method, using the pipeline stage `$lookup` which has 4 fields.**

The $pipeline stage `$lookup` can be thought of as similar to a `join` in MySQL. The `aggregate()` method takes an array as the pipeline parameter.   
With the `$lookup` pipeline stage, `from` is the collection in which to perform the lookup, `localField` is the value(s) being searched for, `foreignField` is the field to search for the `localField` value(s) in and `as` is any string provided as the name of the output.

  
[$lookup](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/) is used to perform an equality match between a field from the input documents (localField) with a field from the documents of the “joined” collection (foreignField).
(If an input document does not contain the localField, the $lookup treats the field as having a value of null for matching purposes.)

The $lookup stage has the following syntax:

```json
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}
```
- `from` specifies the collection in the same database to perform the join with.
The from collection cannot be sharded. (ie it cannot be split across multiple servers).
- `localField` is the value to search for.
- `foreignField` is the field to search for the value specified by localField.
- `as` is the name of the output. (i.e the name of fields containing the fields of the lookup). 




Here the nodules field contains the _id of modules. To get the document references

```
{ "_id" : "M100", "module" : "Databases" }
{ "_id" : "M101", "module" : "Java" }
{ "_id" : "G00101224", "name" : "Mary", "modules" : [ "M100", "M101" ] } { "_id" : "G00205266", "name" : "Sarah", "modules" : [ "M101" ] }
```

To return all documents including the complete referenced documents


```json
db.docs.aggregate([ {$lookup: {from:"docs", localField:"modules",foreignField:"_id", as:"Details"}}])
```
`$lookup` looks for each of these values in the _id field of each of the documents in the collection.
when it find a matching document, it adds it to an array with the name specified by in `as` field. (here as details.)


### $lookup (aggregation)

[$lookup (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/) is used to perform an equality match between a field from the input documents with a field from the documents of the “joined” collection, the $lookup stage has the following syntax:

```json
{
   $lookup:
     {
       from: <collection to join>,
       localField: <field from the input documents>,
       foreignField: <field from the documents of the "from" collection>,
       as: <output array field>
     }
}
```


### Embedded Documents vs Referenced Documents

When should embedded documents be used instead of referenced documents and vice versa?
Advantages of using embedded documents is better performance and atomic.
The advantages of using referenced documents is no repetition of data but it is slower and more complex to write the queries.

Embedded documents means mongodB can perform faster queries as all data can be returned in a single query. 
Embedded data models makes is possible to update documents in a single atomic write operation. Atomic is like a transaction - either all the documents including the embedded ones are updates or none are. 

It is slower to get data from referenced documents than embedded documents as documents must be joined. However if a document is referenced then it is not being repeated many times like an embedded document. As well as being slower, referenced documents are more difficult to write and maintain.
Using referenced documents makes the database more like a relational database than embedded documents.


### MongoDB vs MySQL

When should MongoDB databases be used and when should MySQL databases be used?

- MongoDB better to use when huge amounts of data are being stored and when the amounts being stored can increase dramatically in a relatively short period of time. - If the data to be stored doesn't have a consistent structure or one that is constantly changing then MongoDB is preferable.
- While you can use document referencing, MongoDB does not have the strict foreign key constraints that are in MySQL. This may be a problems for scenarios when you want to ensure double entry accounting , as you want to ensure that a value you put into a record actually exists in the database.

- MySQL is a very stable product and has been around for decades.
- MySQL is a very good option for data that is very structured and controlled. By using data types and foreign keys it can ensure integrity. 
- Where data integrity and security is highly important, MySQL is the better option.

See [introduction to MongoDB](https://docs.mongodb.com/manual/introduction/). The advantages of using documents are they correspond to native data types in many programming languages. Embedded documents reduce the need to expensive joins. Using embedded documents reduce input and output activity  on database systems.
***
## Importing a database into MongoDB

See [mongoimport](https://docs.mongodb.com/manual/reference/program/mongoimport/index.html)
>The mongoimport tool imports content from an Extended JSON, CSV, or TSV export created by mongoexport, or potentially, another third-party export tool. `mongoexport` exports a database.
`mongoimport` is run from the system command line, not the mongo shell.

On a mac if `brew` was used to install mongodb then `mongoimport` is located in `/usr/local/bin/. On windows `mongo import.exe` program is usually located in program files or wherever it is installed in your system.


