## Installing MongoDB
- [Install mongoBD on os-x](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

- [download mongoDB](https://www.mongodb.com/download-center/community)

## Starting MongoDB

To start run the `mongod` command and in another terminal run `mongo` but this doesn't work for me.
See [zellwk](https://zellwk.com/blog/install-mongodb/)
On Mac using brew services instead now.

run `brew services run mongodb-community` in Terminal. This starts MongoDB as a background service.

(Note `start` can be used instead of `run` in the command to start MongoDB automatically when logging in to Macbook.)

To check if MongoDB is running ` brew services list`. This will show the status `started` if it is.
If MongoDB is running, can access the Mongo shell with the `mongo` command.

To quit from the mongo shell, enter `quit()` command to exit mongo.

## Stopping MongoDB

`brew services stop mongodb-community` 

Following the advice of Zell on zellwk.com I have created aliases for the commands above in Terminal.
`$ alias mongod-start='brew services run mongodb-community'`
`$ alias mongod-status='brew services list'`
`$ alias mongod-stop='brew services stop mongodb-community'`

- A **document** is a record in a MongoDB collection and the basic unit of data in MongoDB (analagous to JSON objects or records in a relational database).
- A **collection** is a grouping of MongoDB documents (analagous to tables in a relational database)
- A collection exists within a single database.
- Collections do not enforce a schema. Documents within a collection can have different fields.
- Typically, all documents in a collection have a similar or related purpose.
- A number of **databases** can be run on a single MongoDB server.
- Saving a document to a collection is analagous to inserting a record into a relation. You must also state which database to save to. Note that `db` is not the name of the database but a reference to the current database     
## Commands

- `show dbs` Show databases
- `use myDB` Switch to database 'myDB' if it exists. If it does't already exist, Mongo creates it.
- `db` to show current database (like select database)
- `show collections` to show collections in the current database (like show tables)
- `save()` to create a document. Note a document must have an `_id` field and one will be automatically generated if it is not provided.
- `find()` to query the database. The `find` method finds data in a collection. If no parameters are passed (or an empty document) then all documents in the collection will be returned. Also need to state which collection and which database to find the document in.
- `db.User.find()` where db refers to the current database ("MyDB"), `User` is the name of the collection to find the documents in. `find` is the name of the method.
- `db.User.find().pretty()` to make the results returned easier to read.
- The number of documents returned by a `find` can be limited by providing a query to it. 
- `$and`, `$or` operators to filter the query by name : value pairs
- `$in` operator to filter by an array of values
- `$exists` operator to find documents with specific attributes

- `findOne()` to returned the first document that matches the query
- `sort()` method can be used with the `find()` method to sort the results.

- `save()` 

Note if you pass a document id to the `save` method where the id already exists, it overwrites the existing document. The `save` method calls one of two method `insert` or `update`. `save()` is a **wrapper method** whose main purpose is to call another method. Wrappers in programming are used to hide or abstract details.

- `insert()` to insert a document or documents into a collection.
- To insert multiple documents, pass them to the insert method in an array. An array is an ordered collection of data in square brackets. The attributes of each document do not have to be the same.
- `update()` modifies an existing document or documents in a collection. `update(query, update, options)`

- The `$set` operator is used to replace the value of a field with the set parameter. If the field does not already exist then it will add new fields with the specified values.

- `multi` can be set to true to update all documents. By default it is set to false.
- `deleteOne()` removes a single document that matches the filter (the query) from a collection.
- `deleteMany()` removes all documents that match the filter from a collection. 


**Query operators** provide ways to locate data within the database and  **projection operators** modify how data is presented. See [Query and Projection operators](https://docs.mongodb.com/manual/reference/operator/query/)


```json
db.User.save( 
{ 	_id:1,
	first_name : "John", 
	surname : "Smith", 
	email : "john@gmail.com"
})
```

- [All operators](https://docs.mongodb.com/manual/reference/operator/)

- [Update operators](https://docs.mongodb.com/manual/reference/operator/update/%23id1)

- [Logical Query Operators](https://docs.mongodb.com/manual/reference/operator/query-logical/)

- [Comparison Query Operators](https://docs.mongodb.com/manual/reference/operator/query-comparison/)


## .save() 

```json
db.docs.save({_id:100, fname:"Sean",surname:"Murphy",age:21,email:"seanmurph@yahoo.com",carReg:"04-WH-235"})
db.users.save({_id:100, fname:"John",surname:"Smith",age:33,email:"jsmith@gmail.com",carReg:"131-G-101"})
db.users.save({_id:102, fname:"Aine",surname:"Browne",age:23,email:"abrowne@gmail.com"})
```

## find(query, projection)

Can also use find method with projections to return only certain attributes using `find(query, projection)`
The syntax of the find method is `find(query, projection)` where the query is what you are looking for - whatever documents match this query is returned. The query parameter is an optional parameter. 

The projection determines which fields are returned in the matching documents and is also an optional parameter. The projection is similar to the select clause is mysql

- find all documents in the `users` collection

```json
db.users.find()
```

- find all documents in the `users` collection where the age is 20.

```json
 db.users.find({age:20})
 ```

## Using `$gt` operator

- find all documents in the `users` collection where the age is greater than 20.
**$gt:** operator

```json
db.users.find({age:{$gt:20}})
```

- find all documents in the users collection where the age is greater than 20 and the user has a car.

## Using `$gt` and `$exists` operators

`$gt` matches values that are greater than a specified value.

```json
db.users.find({age:{$gt:20},carReg:{$exists:true}})
```

- find all documents in the users collection where _id is greater than 104 and age is greater than 20.

```json
db.users.find({_id:{$gt:104},age:{$gt:20}})
```

## Using `$and` with the `find()` method.

A compound query can specify conditions for more than one field in the collection’s documents. Implicitly a logical connects the clauses of a compound query so that the query selects the documents in the collection that match all the condition

```json
db.inventory.find( { status: "A", qty: { $lt: 30 } } )
```
is equivalent to 

```sql
SELECT * FROM inventory WHERE status = "A" AND qty < 30
```

```json
db.users.find({$and: [{email: {$exists: true}}, {age: {$gt: 20}}]})
```



*Return only the email attribute of documents where the age is greater than 18 you supply two parameters to the find method.* 

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

```json
db.inventory.find( { status: { $in: [ "A", "D" ] } } )
```

corresponds to `SELECT * FROM inventory WHERE status in ("A", "D")` in SQL.
This finds all the documents from the inventory collection where status equals "A" or "D".
Although this query could also be expressed using the `$or` operator, the  manual recommends using the `$in` operator when performing equality checks on the same field.


## $or operator
The `$or` operator can be used to specify a compound query. [`$or`](https://docs.mongodb.com/manual/reference/operator/query/or/#op._S_or) joins each clause with a logical OR so the query selects documents in the collection that match at least one condition. 

```json
db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )
```

This retrieves all documents in the collection where the status equals "A" or qty is less than ($lt) 30 and corresponds to the following SQL:
```sql
SELECT * FROM inventory WHERE status = "A" OR qty < 30
```

## AND and OR conditions can be used together.

```json
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
})
```
corresponds to 

```sql
SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")
```


## Match an Array

See [query an array](https://docs.mongodb.com/manual/tutorial/query-arrays/). 
You can specify an equality condition on an array using the query document { <field>: <value> } where <value> is the exact array to match, including the order of the elements.

```json
db.inventory.find( { tags: ["red", "blank"] } )
```
This queries all documents where the field `tags` value is an array with exactly two elements, "red" and "blank", in the order as specified.

If the order doesn't matter use the `$all` operator.
```json
db.inventory.find( { tags: { $all: ["red", "blank"] } } )
```



## `findOne()`
- find the first document in the users collection where the user has a car.

```json
db.users.findOne({carReg:{$exists:true}})
```

## `save()` 
- User 106 - Shane has bought a car with reg 12-G-1234. The following command was run to update the user’s document: 
```json
db.users.save({_id:106, carReg:"12-G-1234"})
```

What does the document look like now and why?

The document for user 106 was as follows before the `.save()`
> { "_id" : 106, "fname" : "Shane", "surname" : "Kelly", "age" : 24, "email" : "sk998@yahoo.com" }

The document for this user has been overwritten with these name:value pairs. All other details for this user have been overwritten.
>{ "_id" : 106, "carReg" : "12-G-1234" }

## `update()` command with the `$set` operator
If you pass a document id to the `save` method where the id already exists, it overwrites the existing document. The `save` method calls one of two method `insert` or `update`. Save is a **wrapper method** whose main purpose is to call another method. Wrappers in programming are used to hide or abstract details.

- User 102 - Aine has bought a car with reg 10-G-9876. The following command was run to update the user’s document: 
```json
db.users.update({_id:102}, {carReg:"10-G-9876"})
```
What does the document look like now and why?

Before the update the document for user with id 102 is:
`db.users.find({_id:102})`
>{ "_id" : 102, "carReg" : "10-G-9876", "age" : 1, "sex" : "M" }

After the update:
`db.users.update({_id:102}, {carReg:"10-G-9876"})`
> WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 1 })

`db.users.find({_id:102})`
> { "_id" : 102, "carReg" : "10-G-9876" }

`update` and `save` did the exact same thing here.  **Without using the $set operator, the whole document would be replaced.**


- User 105 – Bill’s document is as follows:
>{ "_id" : 105, "fname" : "Bill", "surname" : "Mulligan", "age" : 19, "email" : "billy123@gmail.com" }
Bill has bought a car with reg 161-MO-4. Give the command so that Bill’s document now looks as follows:
>{ "_id" : 105, "fname" : "Bill", "surname" : "Mulligan", "age" : 19, "email" : "billy123@gmail.com", "carReg" : "161-MO-4" }

Using `$set`, if the attribute exists it changes it to the new value, otherwise it adds the new attribute and it's value. Without using the $set operator, the whole document would be replaced as was the case for the previous two examples.

```json
db.users.update({_id:105},{$set:{carReg:"161-MO-4"}})
```

db.docs.update({_id:1},{$set:{carReg:"191-K-4"}})

>WriteResult({ "nMatched" : 1, "nUpserted" : 0, "nModified" : 0 })
```json
db.users.find({_id:105})
```
> { "_id" : 105, "surname" : "Mulligan", "age" : 20, "email" : "billy123@gmail.com", "carReg" : "161-MO-4", "sex" : "M", "Name" : "Bill" }
> 

- Add original fields back to user 106.

## Updating several attributes at the same time:


```json
db.docs.update({_id:201}, {$set:{fname:"Shane",Surname:"Kelly",age:24,email:"sk998@yahoo.com"}})
```

## Updating an attribute for all documents in the collection 
Using **`multi:true`** with `update()` or **`updateMany()`** command.
- Give the mongodb command to add 1 to each user’s age.

Set the **`multi`** paramater to true to update all documents. Otherwise only the first document will be updated

`db.docs.update({},{$inc:{age:1}})` only update the first age in the first document.

See [multi](https://docs.mongodb.com/manual/reference/method/db.collection.update/#db.collection.update)

## `multi:true`

```json
db.docs.update({},{$inc:{age:1}},{multi:true})
```

## `updateMany()`
`updateMany()` does the same thing as update with multi:true

`db.users.updateMany({},{$inc:{age:1}})`

## Add a new attribute to each document (some with different values):

## using the `$in` operator
`$in` matches any of the values specified in an array.

- Add a new attribute sex, to each document where the sex is set to M for most user id's.

Using the `$in:` operator which is a comparison operator. This can be used to update any documents with an id in the array provided to `$in:`.

**Use $set to not overwrite the other attributes for each document.**

```json
db.users.updateMany({_id:{$in:[101,102,103,105,106,107]}},{$set:{sex:"M"}})
```

## using `$ne` (not equal to operator)

`$ne` matches all values that are not equal to a specified value.

Where the sex is not already equal to male, set it to female.
```json
db.users.updateMany({sex:{$ne:"M"}},{$set:{sex:"F"}})
```

## using `$and` operator

- Add a new attribute title  with the value Mr., to each document where the sex is M, and the age is greater than 20:

See [$and operator](https://docs.mongodb.com/manual/reference/operator/query-logical/)
`$and` - joins query clauses with a logical AND returns all documents that match the conditions of both clauses.

`{$and:[{sex:"M"},{age:{$gt:20}}]}`

```json
db.users.updateMany({$and:[{sex:"M"},{age:{$gt:20}}]},{$set:{title:"Mr. "}})

```
## Remove attribute from specified documents using `$unset` operator

See [Update Operators](https://docs.mongodb.com/manual/reference/operator/update/#id1), specifically [$unset:](https://docs.mongodb.com/manual/reference/operator/update/unset/#up._S_unset).

`$unset` removes the specified field from a document.


- Users 101 – Sean, 103 – Alan and 107 – Will have sold their cars, update the collection to remove the carReg attribute from these documents.


```json
db.users.update({$or:[{_id:101},{_id:103},{_id:107}]},{$unset:{carReg:""}},{multi:true})
```

## show certain attributes for documents with specific ids.

- Show only the fname, surname, age and sex attributes of documents where the _id is between 101 and 107 inclusive.

See [collection methods](https://docs.mongodb.com/manual/reference/method/#collection) and [db.collection.find()](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find)

Note the `_id` field is alwats returned by the `find()` method unless the `_id` field is set to `0` which will suppress the field.



```json
db.users.find({$and:[{_id:{$gte:101}},{_id:{$lte:107}}]},{fname:1, surname:true, age:true,sex:1})
```

## Specify that the `_id` field is not to be returned

The default is to return the `_id` field. To not return it, set it to 0 `_id:0`


> db.users.find({$and:[{_id:{$gte:101}},{_id:{$lte:107}}]},{fname:1, surname:true, age:true,sex:1, _id:0})


## Rename an attribute

`$rename` update operator renames a field.

```json
db.users.updateMany({},{$rename:{fname:"Name"}})

```

***

## Importing a database into mongo

`(base) Angelas-MBP:bin angelacorkery$ mongoimport --db=mydemo --collection=docs --file=/Users/angelacorkery/downloads/demo1b.json`

See [mongoimport](https://docs.mongodb.com/manual/reference/program/mongoimport/index.html)
>The mongoimport tool imports content from an Extended JSON, CSV, or TSV export created by mongoexport, or potentially, another third-party export tool. `mongoexport` exports a database.
`mongoimport` is run from the system command line, not the mongo shell.

On a mac if `brew` was used to install mongodb then `mongoimport` is located in `/usr/local/bin/. On windows `mongo import.exe` program is usually located in program files or wherever it is installed in your system.

if a database called demo1b.json is located in my downloads folder, cd to the `/usr/local/bin` folder where mongoimport is located.


(base) A's-MBP:bin an..c..$ `mongoimport --db=mydemo --collection=docs --file=/Users/angelacorkery/downloads/demo1b.json`

bin ang... $ mongoimport --db=mydemo --collection=docs --file=/Users/ang.../downloads/demo1a.json`

[db.collection.find](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find)

$ `mongoimport --db=mlab7 --collection=lab7 --file=/Users/an.../downloads/lab7.json`

##### find(query,projection)
```json
db.docs.find({},{_id:0,surname:1})
```
This uses a projection together with the query to only return the surname of everyone in the collection. The `_id` field is set to 0 so that the id field is not returned.

##### .sort()

```json
db.docs.find({age:{$gt:21}},{_id:0, fname:1,surname:1}).sort({surname:1, fname:1})
```
This show only fname and surname fields of all people aged 21 or older. Sort the results in ascending surname and within surname on descending fname order

***

## Index

- By default the only index on a document is on the _id field.

- To find the indexes on a collection: `db.Collection.getIndexes()`
- Which returns information in the following format, detailing the index field (_id) and the order of the indexes (1 is ascending; -1 is descending:

```
"key" : {
	"_id" : 1
},
```

To get the name and type of the index on the collection use `getIndexes()`

`db.docs.getIndexes()`

[
	{
		"v" : 2,
		"key" : {
			"_id" : 1
		},
		"name" : "_id_",
		"ns" : "docs1.docs"
	}
]
`db.users.getIndexes()`
{
		"v" : 2,
		"key" : {
			"_id" : 1
		},
		"name" : "_id_",
		"ns" : "usersDB.users"
	}

***
# Aggregate()

- [db.collections.aggregate](https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#db.collection.aggregate). 
- [db.collection.aggregate() Stages](https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/#db-collection-aggregate-stages) 

The **aggregate()** method calculates aggregate values for the data in a collection such as min, max, average etc.

The `aggregate()` method takes 2 parameters. 
- The **pipeline stages** parameter is an array of options or **stages**, 
- The **pipeline operators** which is an optional parameter and can be used to change the way the aggregation method works.


- `$group` is an aggregation pipeline *stages*. It works the same as `group by` in MySQL. 
- The value of $group is a document. 
- `_id` is mandatory and is the documents you wish to group by, Can set the `_id` to **null** so as not to aggregate by any particular ids. 

- When using `aggregate` you need to put a dollar sign in front of the field.

In this example Average is the string we want to return the results as. It can be any string.
`$gpa` is the attributes to get the average of.

`Average: {$avg: "$gpa"}` to get the average gpa for all students and return in as 'Average'

```json
db.users.aggregate([{$group : {_id: null, Average: {$avg: "$gpa"}}}])
```

```json

```json
db.march.aggregate([{$group : {_id:"$age", "Max GPA per Age": {$max: "$gpa"}}}])
```
- This gets the maximum gpa grouped by age group.

##### aggregate sum but not grouped by anything

```json
db.docs.aggregate([{$group:{_id:null, "Total Age":{$sum:"$age"}}}])
```
- to show the combined ages of everyone in the collection as "Total Age".
- Here the `_id` is `null` as we don't want to group it by anything. 



[db.collection.aggregate() Stages](https://docs.mongodb.com/manual/reference/operator/aggregation-pipeline/#db-collection-aggregate-stages)
The aggregate method takes one parameter which is an array. For this interested in the aggregate pipeline stage
For $group have to specify an id. 
**Note when using `aggregate` you need to put a dollar sign in front of the field.**

`db.collection.aggregate( [ { <stage> }, ... ] )`

-[{ $sum: <expression> }](https://docs.mongodb.com/manual/reference/operator/aggregation/sum/)


{ "_id" : null, "Total Age" : 207 }

to do it by sex. For attributes that had an attribute of null for the sex field are not included.

```json
db.docs.aggregate([{$group:{_id:"$sex", "Total Age":{$sum:"$age"}}}])
```

> db.docs.aggregate([{$group:{_id:"$sex", "Total Age":{$sum:"$age"}}}])
{ "_id" : null, "Total Age" : 0 }
{ "_id" : "M", "Total Age" : 122 }
{ "_id" : "F", "Total Age" : 85 }

This is like the `groupby` in mysql.


***

## Embedded documents.

```json
db.docs.find({"engine.bhp":{$gt:115}})
```
- *To show the registration, make and model for all cars where the bhp is over 115.*
 Here `bhp` is a sub-document of (or contained within) the `engine` document so use `"engine.bhp"`.
The projection is another document. `bph` is part of an embedded document so have to access it in a slightly different way using the dot notation with quotes around it as `"engine.bhp"`.


>{ "_id" : "02-D-23212", "make" : "Ford", "model" : "Focus", "engine" : { "size" : 1.3, "zeroToSixty" : 10.6, "bhp" : 118 } }
>{ "_id" : "191-D-102", "make" : "Toyota", "model" : "Corolla", "engine" : { "size" : 1.4, "zeroToSixty" : 10.5, "bhp" : 118 } }
>{ "_id" : "11-G-987", "make" : "Ford", "model" : "Mondeo", "engine" : { "size" : 1.6, "zeroToSixty" : 8, "bhp" : 120 } }

```json
db.docs.find({"engine.bhp":{$gt:115}},{make:true, model:true,_id:true})
```

>{ "_id" : "02-D-23212", "make" : "Ford", "model" : "Focus" }
>{ "_id" : "191-D-102", "make" : "Toyota", "model" : "Corolla" }
>{ "_id" : "11-G-987", "make" : "Ford", "model" : "Mondeo" }



### Aggregation Pipeline Stages `$group(aggregation)`
- *Show the average bhp for each make of car.*

```json
db.docs.aggregate([{$group:{_id:"$model","Avg BHP":{$avg:"$engine.bhp"}}}])
```

This uses [$group (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/group/#pipe._S_group). The $group **stage** has the following prototype form:

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
- Accumulator operators include `$avg` for averages, `$min`, `$max`, `$sum`, `$first` and `$last`.

```json
db.docs.aggregate([{$group:{_id:"$model","Avg BHP":{$avg:"$engine.bhp"}}}])
```
returns the average bhp for each model of car as "Avg BHP".

>{ "_id" : "Fiesta", "Avg BHP" : 88 }
{ "_id" : "Mondeo", "Avg BHP" : 120 }
{ "_id" : "Corolla", "Avg BHP" : 118 }
{ "_id" : "Prius", "Avg BHP" : 90 }
{ "_id" : "Focus", "Avg BHP" : 118 }

***
##  $lookup (aggregation)

[$lookup](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/) performs a left outer join to an unsharded collection in the same database to filter in documents from the “joined” collection for processing.

*Show the details of all books and for each book also show all details of the corresponding author as "Written by". Sort the results by authors name.*

```json
db.docs.aggregate([{$lookup:{from:"docs" ,localField:"author", foreignField:"_id",as:"Written by"}}])
```
[$lookup (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/)
> To perform an equality match between a field from the input documents with a field from the documents of the “joined” collection, the $lookup stage has the following syntax:

```
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

### $sort (aggregation)

- An aggregation [$sort (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/sort/) can be used to sort all input documents and return them to the pipeline in sorted order.
(This is not the same as the ordinary `sort` method).
- $sort takes a document that specifies the field(s) to sort by and the respective sort order.
	- `1` for ascending 
	- `-1` for descending  

```json
db.users.aggregate(
   [
     { $sort : { age : -1, posts: 1 } }
   ]
)
```
This sorts the documents in the users collections in descending order by the age field and then in ascending order by the posts field.


```json
db.docs.aggregate([{$lookup:{from:"docs" ,localField:"author", foreignField:"_id",as:"Written by"}},{$sort:{"Written by.name":1}}])
```
*Show the details of all books and for each book also show all details of the corresponding author as "Written by". Sort the results by authors name.*

```json
db.docs.aggregate(
	[{$lookup:{from:"docs" ,localField:"author", foreignField:"_id",as:"Written by"}},
	 {$sort:{"Written by.name":1}}
	]
)
```
This example of aggregation uses two aggregations, `$lookup` and then `$sort`. 
The `$sort` is a document, the field to sort on here is "name" and the sort order is ascending (1). 


 > db.docs.aggregate([{$lookup:{from:"docs" ,localField:"author", foreignField:"_id",as:"Written by"}},{$sort:{"Written by.name":1}}])
{ "_id" : 2, "name" : "C.S. Lewis", "born" : "England", "Written by" : [ ] }
{ "_id" : 3, "name" : "John McGahern", "born" : "Ireland", "Written by" : [ ] }
{ "_id" : 1, "name" : "J.K. Rowling", "born" : "England", "Written by" : [ ] }
{ "_id" : 101, "title" : "The Lion, the witch and the wardrobe", "author" : 2, "Written by" : [ { "_id" : 2, "name" : "C.S. Lewis", "born" : "England" } ] }
{ "_id" : 102, "title" : "The House and his boy", "author" : 2, "Written by" : [ { "_id" : 2, "name" : "C.S. Lewis", "born" : "England" } ] }
{ "_id" : 103, "title" : "Harry Potter and the Philosopher's Stone", "author" : 1, "Written by" : [ { "_id" : 1, "name" : "J.K. Rowling", "born" : "England" } ] }
{ "_id" : 100, "title" : "That They May Face the Rising Sun", "author" : 3, "Written by" : [ { "_id" : 3, "name" : "John McGahern", "born" : "Ireland" } ] }


***
$ `mongoimport --db=mlab7 --collection=lab7 --file=/Users/an.../downloads/lab7.json`

- ` show dbs` to see what databases are there.
- `use lab7` to use lab7 database
- ` show dbs` to see what databases are there.
- `use lab7` to use lab7 database

- With the `use` command, if the database named doesn't already exist, mongodb will create the database.
- `db` always refers to the current database. The `db` command will return the current db.
- `show collections`
- `db.docs.find()`

## find(),	$gt, 	$exists,   $and

- **Show the name and population of all cities where the population is over 10,000**

```json
db.docs.find({pop:{$gt:10000},city:{$exists:true}},{_id:0, city:1, pop:1})
``` 

or using the $and operator which takes in an array [] of sub-documents.
Note in the query above the city field is not inside a sub-document. Instead all the fields are in the one query separated by commas.
When using the `$and` operator, city is inside a sub-document.

```json
db.docs.find({ $and:[{pop:{$gt:10000}},{city:{$exists:true}}]},{_id:0, city:1, pop:1})
```
 
Both give the same results.

>{ "city" : "PROVIDENCE", "pop" : 31069 }
{ "city" : "AGAWAM", "pop" : 15338 }
{ "city" : "CRANSTON", "pop" : 25668 }
{ "city" : "NEW YORK", "pop" : 18913 }
{ "city" : "MIAMI", "pop" : 47761 }

(Look at and operator documentation again)

## $group(aggregation),  $match(aggregation),  $exists

- **Show the name and population of each state based on the cities shown.**

There are a number of different cities in each state so need to use the `aggregate` method here. 
See [$group (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/group/)

Aggregate takes one parameter which is an array which takes at least one sub-document. {}
Using the $group pipeline stage. 

See [$match (aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/match/)
Only want to pass those with a city into the group stage. 
$match takes a query. only want documents that have an attribute city.

`$match` filters the documents to pass only the documents that match the specified condition(s) to the next pipeline stage. `{ $match: { <query> } }` . 
- `$match` takes a document that specifies the query conditions.

Here the match takes the city field exists

```json
db.docs.aggregate([{$match: {city:{$exists:true}}},{$group:{_id:"$state","Total Pop":{$sum: "$pop"}}}])
```

>{ "_id" : "RI", "Total Pop" : 56737 }
{ "_id" : "FL", "Total Pop" : 64691 }
{ "_id" : "NY", "Total Pop" : 23681 }
{ "_id" : "MA", "Total Pop" : 19212 }


- Inside `$group` the `_id` is what you want to group by, in this case by state in quotes ("state")
- "Total Pop" is what you want the results returned as. 
- The value is a document, inside of which is the accumulator, `$sum`. 
- The field to sum up is "pop"

Note without using the `$match` aggregation on the city field, the incorrect results are returned below as the aggregation is picking up extra fields. Too many documents are going into the group by clause. In some documents the state field is the foundation year of the state. Using `$match` with the city field would stop these extra fields from getting past the pipelin group stage.

```json
db.docs.aggregate([{$group: {_id: "$state","Total Pop":{$sum: "$pop"}}}])
```

> db.docs.aggregate([{$group: {_id: "$state","Total Pop":{$sum: "$pop"}}}])
{ "_id" : 1845, "Total Pop" : 6800000 }
{ "_id" : null, "Total Pop" : 0 }
{ "_id" : "RI", "Total Pop" : 56737 }
...
{ "_id" : "NY", "Total Pop" : 23681 }
{ "_id" : 1788, "Total Pop" : 28300000 }

- **Show the total population of cities in NY as “Population”.**

Similar to above query but limiting the documents being passed into the group by stage by state being New York. 
- Using `$match` which takes a query. 
- Adds two conditions into the query given to match, that city exists and that state is NY.
- `$match: {city:{$exists:true},state:"NY"}}`

```json
db.docs.aggregate([{$match: {city:{$exists:true},state:"NY"}},{$group:{_id:"$state","Total Pop":{$sum: "$pop"}}}])
```

Note that here you could leave out city exists and get the same results.
```json
db.docs.aggregate([{$match: {state:"NY"}},{$group:{_id:"$state","Total Pop":{$sum: "$pop"}}}])
```

{ "_id" : "NY", "Total Pop" : 23681 }

### Embedded (sub) documents
- **Show the _id, city and name of the capital city of each state for cities with a population greater than 20,000.**

 

The name field is not part of the outer document. The only attributes of the outer document are _id, city, pop, state and capital. The capital name is part of an embedded or sub-document so need to use "capital.name" as name is part of the document that is embedded in the document.


```json
db.docs.find({city:{$exists:true},pop:{$gt:20000}},{city:1,"capital.name":1})
```
{ "_id" : "02906", "city" : "PROVIDENCE", "capital" : { "name" : "Providence" } }
{ "_id" : "02907", "city" : "CRANSTON", "capital" : { "name" : "Providence" } }
{ "_id" : "33125", "city" : "MIAMI", "capital" : { "name" : "Tallahassee" } }


## $lookup aggregation

- **Show all details for “Tom” including full details of his addresses.**

```json
db.docs.aggregate([{$match: {name:"Tom"}},{$lookup: {from:"docs",localField:"addresses",foreignField:"_id", as:"Lived In"}}]).pretty()
```

[$lookup(aggregation)](https://docs.mongodb.com/manual/reference/operator/aggregation/lookup/) consists of 4 parameters.

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

- `aggregate` takes one parameter which is an array and at least one aggregation stage, which here is $lookup.
The foreign field is `_id` 

Need to pass documents to the aggregation stage only where the name is Tom so using the [$match aggregation](https://docs.mongodb.com/manual/reference/operator/aggregation/match/) stage here to filter the documents. 

```json
db.docs.aggregate([{$lookup:{from:"lab7", localField:"addresses", foreignField:"_id", as:"Lived In"}}])
```
$match limits what goes into the query. only do a lookup for documents that pass by the match stage.

```json
db.docs.aggregate([{$match:{name:"Tom"}},{$lookup:{from:"lab7", localField:"addresses", foreignField:"_id", as:"Lived In"}}])

```
```json
db.docs.aggregate([{$match: {name:"Tom"}},{$lookup: {from:"docs",localField:"addresses",foreignField:"_id", as:"Lived In"}}]).pretty()
```
{
	"_id" : "1",
	"name" : "Tom",
	"addresses" : [
		"01001",
		"12997"
	],
	"Lived In" : [
		{
			"_id" : "01001",
			"city" : "AGAWAM",
			"pop" : 15338,
			"state" : "MA",
			"capital" : {
				"name" : "Boston",
				"electoralCollege" : 11
			}
		},
		{
			"_id" : "12997",
			"city" : "WILMINGTON",
			"pop" : 958,
			"state" : "NY",
			"capital" : {
				"name" : "Albany",
				"electoralCollege" : 29
			}
		}
	]
}

## $project aggregation pipeline stage,   $match,  $lookup

- **Show all details for “Chesterfield” including full details of the state, but do not show details relating to its capital**.

```json
db.docs.find({city:"CHESTERFIELD"})
```
>{ "_id" : "01012", "city" : "CHESTERFIELD", "pop" : 177, "state" : "MA", "capital" : { "name" : "Boston", "electoralCollege" : 11 } }

We want to replace the "MA" with the actual state.

- Use the [$project aggregation pipeline stage](https://docs.mongodb.com/manual/reference/operator/aggregation/project/). It includes or excludes fields from a projection.
- In this case, exclude the capital field from the projection using `{$project:{capital:0}}`

```json
db.docs.aggregate([{$match: {city:"CHESTERFIELD"}},
					{$lookup:{from:"docs",localField:"state",foreignField:"_id", as:"State"}},
					{$project:{capital:0}}])
```
>{ "_id" : "01012", "city" : "CHESTERFIELD", "pop" : 177, "state" : "MA", "State" : [ { "_id" : "MA", "name" : "Massachusetts", "pop" : 6868000, "state" : 1790 } ] }

Here without excluding the capital city details.
```json
db.docs.aggregate([{$match: {city:"CHESTERFIELD"}},
				   {$lookup:{from:"docs",localField:"state",foreignField:"_id", as:"State"}}])
```
returns
>{ "_id" : "01012", "city" : "CHESTERFIELD", "pop" : 177, "state" : "MA", "capital" : { "name" : "Boston", "electoralCollege" : 11 }, "State" : [ { "_id" : "MA", "name" : "Massachusetts", "pop" : 6868000, "state" : 1790 } ] }








