MongoDB
=======

*MongoDB in 45 minutes* is our Database Systems Laboratory project.

Our goal is to introduce the pros and cons of an alternative way of data storing - NoSQL, document database.
>If you got tired of traditional SQL systems, you could not find a better place to brush up your knowledge. We will change your point of view and ensure you that working with databases can be a pleasure. 
>If you are new to database systems - it is good for you as well, thanks to our guidance you will never use any database system other than MongoDB! 

Take a while to clone, read & run, after 45 minutes you will be running your own web service based on Node.js and MongoDB.
Firstly we will satisfy you with a bit of theory and then we will show you how to configure and run the system just in a few steps.

Experience the power and simplicity of MongoDB!

Note: The entire course is included in this repository. After clone you can work locally, please follow REAMDE file :).

Introduction
----

### Basic facts

Some facts about MongoDB:
* cross-platform document-oriented database system
* world's most popular NoSQL database
* fast, scalable, available

What does it all mean?

### NoSQL

Traditional database systems use *relational model*:
* data organized in *tables*
* each table has a set of *fields* - the structure of each record in table is set
* relationships between tables make complex queries possible
* queries to most relational databases are made using SQL.

MongoDB uses a *document-oriented* approach:
* data is kept in *documents*, organized in *collections*
* collections do not enforce document structure
* user can choose a data model that satisfies his needs best
  * document relationships
  * document embedding 
* no structure enforcement - no *join* queries

### Performance, availability, scalability

MongoDB includes mechanisms for increasing the database's performance and availability even in large systems. These are:

1. Replication
 * multiple copies of the database on different servers
 * provides data redundancy -> security
 * increases availability - read operations can be performed on any replica
2. Sharding
 * provides *horizontal scaling* - divides the data set across multiple servers (*shards*)
 * reduces the number of operations and data stored per shard

SQL vs. NoSQL
---

### Where to NoSQL


The greatest strength of MongoDB's document-based approach is its flexibility. Each data item can have its own structure, which makes representing real-life objects with ease.  
Imagine a database storing information about school students and their equipment. Although some basic information about students has similar structure (e. g. name, year etc.), the students' equipment may vary. One student may have a school bag full of notebooks, a pencil case with pens and pencils etc., and another may choose to bring just his laptop. In a relation-based approach we would have to use many tables with many colums to account for all possibilities - in MongoDB, we don't have to worry about anything - the data can have any form we want!

### Where not to NoSQL

NoSQL databases, including MongoDB, give up on the advantages of the rigid structure of the relational databases in the name of flexibility. MongoDB does not support queries to more than one collection at once (similar to SQL JOIN queries). All MongoDB operations are atomic only per document - there is no way to enforce transactionality. It means it cannot be used in applications which require these features.

Some technical details
----

### Data representation

As mentioned before, MongoDB stores data as *documents*, organized loosely in *collections*. Every document is stored in database in BSON format. *BSON* = binary + JSON - binary representation of extendced JSON used by MongoDB.

### Queries

Queries for MongoDB are written in JavaScript and give results in JSON format (query results are, in fact, documents themselves). This allows for seamless integration with applications written in JavaScript.

Each query is conducted on a given collection. There is no way to refer to more than one collection in one query - to achieve a fuctionality similar to SQL JOIN one has to make more than one query to the database.

Write operations are atomic only with respect to a single document. It means that it is impossible to enforce full transactionality in MongoDB. It can be viewed as a trade-off between 

Let's code
----

Now the most interesting part of our tutorial. 
We will show you how to configure your environment, how to run your MongoDB database and how to store and query some data. 
In the end of our tour you will run the web service to illustrate examples from the introduction part.

OK, let's do it!

MongoDB configuration
----

Now we will install MongoDB on your computer. Please be sure you are connected to the internet.

###System requirements

We suggest working on a UNIX like system. Following instructions are related to Linux distribution (Ubuntu 12.10).
Please do not panic if you have any other operational system, MongoDB can be hosted enywhere, so besides installing process, every part of our course can be completed on your machine.

Firstly you need to download and install MongoDB. You can use `apt-get` tool or download binaries driectly from [MongoDB Downloads]. We prefer the first procedure.
```sh
sudo apt-get install mongodb
```
After that you should have totally prepared environment. So easy, isn't it?
Now we will show you how to use `mongo` shell - default MongoDB distribution shell.

###`mongo` shell

`mongo` is a powerful tool, it enables access to JavaScript languafge environment and a full database interface for MongoDB. To perform next steps we assume you have installed MongoDB (see [installing MongoDB](https://github.com/BartoszJanota/MongoDB/edit/master/README.md#system-requirements))

Now you will connect to `mongod` using `mongo` shell.

In your command prompt start `mongo`. Not suprisingly, please type:

```sh
mongo
```

You should be connected to the `mongod` database server listening on port *27017* on the *localhost* interface by default.

Now you can see which database you are connected to:

```sh
db
```

`mongod` uses `test` as a default database.

You can list your databases with:

```sh
show dbs
```
Please, create and swich to a new database:

```sh
use mynewdb
```

Now you can check that you created a proper database by typing:
```sh
sb
```

It will print your current session database context. 

What is interesting, retyping `show dbs` will show you nothing more than the last time, so why? Answer is simple, MongoDB will not persist your database until you insert some data into.

Your first Collection and Inserts
----

In this section you will create your first Documents and Insert them into your database.

###First Collection Insert

Assuming you are still connected to your databas (check `db`, if not, connect your database with `use mynewdb`) you can now prepare some Documents and Insert them.

As we said before, `mongo` let you use JavaScript, so now we can create some variables:

```javascript
tutorial = {name: "my tutorial", subject: "mongodb"}
card = {job: "doctor", seniority: 3}
```
As we have these two documents, we want to store them now, but wait, we still have no collections. Solution is easier than you think, just type:

```sh
db.testCollection.insert( tutorial )
db.testCollection.insert( card )
``` 

These instructions creates the testCollection collection and inserts our documents into, please remember, your database `mynewdb` was phisically created only when you have inserted something into!

It is everything you need to store your data. Please notice, above documents are totally different, their structure is different and have nothing in common, nevertheless, you can just insert them and store in one place (collection). Now you can phisically meet the MongoDB power.

###Through the database

Now as you have inserted some data you can try to list it.

```sh
show collections
```

That instruction will show you all collections you declared in your current database. The only collection in your system is `testCollection`. All `monogod` databases have either `system.indexes` default collection.

You found out that your `testCollection` exists, so now, you can check its content:

```sh
db.testCollection.find()
```

You should see an ouput like this:

```sh
{ "_id" : ObjectId("535e44725dd7f6c31cd0d424"), "name" : "my tutorial", "subject" : "mongodb" }
{ "_id" : ObjectId("535e44725dd7f6c31cd0d425"), "job" : "doctor", "seniority" : 3 }
```

As you can see, all inserted documents must have their own, unique `_id` field.

###Specified queries

In the last section you have learned how to insert some data into you database. Now we will do some more difficult operations.

As we operate in JavaScript environment, we can do:

```javascript
for (var i = 3; i <= 5; i++) db.testCollection.insert( {job: "teacher", seniority: i} )
```

Now we have a bigger collection, so we can browse it.

###The Cursor

Every `mongo` query returns a cursor object that contains the results of the query.
If you have followed our course properly, you should have 5 documents inserted now.

To see how cursor works just try:

```sh
var cursor = db.testCollection.find()
```

Now you can use `cursor` as a simple array:

```sh
printjson( cursor [ 3 ])
```

It should return the 3rd document

###Search criteria

When you wanto find specific documents you can just add additional criteria:

```sh
db.testCollection.find( { seniority: {$gt : 3} } )
```

or

```sh
db.testCollection.find( { seniority: 3 } )
```

You should see some results according to the given criteria.
Try some more spohisticated criteria! Check more at MongoDB [find()](http://docs.mongodb.org/manual/reference/method/db.collection.find/) reference.

Now you are able to create your own databases and collections. You can insert some documents and browse them, we encourage you to practise more and more. In the next section you will see how to use MongoDB together with Node.js quickly and easily.


MongoDB and Node.js integration
----

There are several ways for Node.js to talk to MongoDB:
* **MongoDB node.js driver** - officially supported solution - basic operaions like in Mongo console
* **Mongoose** - object-document mapping - a powerful library for high-level data management

*TO DO*
* download Node.js and other libs
* install
* run
* like http://cwbuecheler.com/web/tutorials/2013/node-express-mongo/

Implementation - example no. 1
----
*TO DO*
* the first moment to complement our code - i.e. student wth a notebook bag
* result


Implementation - example no. 2
----
*TO DO*
* another example
* result

Implementation - final example
----
*TO DO*
* Final result
* Encouregment to further development

Summary
----
*TO DO*
* just a simple summary

Knowledge source
----
* [MongoDB Home]
* [CWBUECHELER] 

License
----

MIT - free to use :)!

by [Bartosz Janota](mailto:bartosz.janota@gmail.com) and [Piotr Mikoda](mailto:piotr.mikoda@gmail.com)

[MongoDB Home]:https://www.mongodb.org/
[MongoDB Downloads]:http://www.mongodb.org/downloads
[CWBUECHELER]:http://cwbuecheler.com/web/tutorials/2013/node-express-mongo/



