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
* 

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

*TO DO*:
* MnogoDB intro
* NoSql
* document-oriented storage
* repliacation, scalability, availibility
* auto-sharding
* querying,
* map-reduce
* etc.

SQL vs. NoSQL
---

*TO DO*:
* SQL
* NoSQL
* diff
* why NoSQL is still better

Where to NoSQL
----

The greatest strength of MongoDB's document-based approach is its flexibility. Each data item can have its own structure, which makes representing real-life objects with ease.  
Imagine a database holding 

*TO DO*:
* simple examples: student with a bag and books, a pencilcase (with a rubber and a pencil) and etc. inside and another one with a notebook bag only - no database schema etc., and very different models of one subject.
* easy general SELECT with no detailed conditions
* etc.

Where not to NoSQL
---

*TO DO*:
* when SELECTing very specified queries or SELECTs with joins
* model architecture that must be mapped on tables
* anything else?

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
mynewdb.testCollection.insert( tutorial )
mynewdb.testCollection.insert( card )
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
mynewdb.testCollection.find()
```

You should see an ouput like this:

*TO DO*
* run an above example

###Specified queries

*TO DO*
* another insert
* conditional select

Webservice configuration
----

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



