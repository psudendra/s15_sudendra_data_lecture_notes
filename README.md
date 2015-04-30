# Lecture Notes for Data Engineering Spring 2015

## Lecture 1 (1/13/2015)
  - All notes must be on GitHub.

  - Data Engineering
    - Social Networks
    - Data Analytics
      - Sampling
      - Machine Learning
      - Can we predict what customers are going to do in the future?
      - Predict random user’s behavior
    - Storage
      - NoSQL
      - Document databases
      - Graph databases
      - Key-value storage
      - Colomner stores (not key-values)
    - Big data
      - Data collection & cleaning
      - How to access it?
      - Has to clean before it can be stored
    - InfoViz
      - Huge data sets, how do you view them to the user?
      - D3 (JS framework)
      - Tablo
      - R

  - Data Life Cycle
      - Question, Curating, Triage, Persistence → Collection → Clean up → Storage → Processing, Analysis → Query, utilize, act
      - Triage: prioritization

  - Request Response Cycle

---
## Lecture 2 (1/15/2015)
#### Github Markdown
* Two types: Github flavored (GFM) and standard (SM)
* Can be used for: styling, word formatting, images, lists (ordered and unordered), links, horizontal lines, tables, code blocks
* Two spaces or two enters create new paragraph

Daring Fireball - markdown

#### HTTP request and response cycle cont'd

Browser <--> Web/App Server <--> Handler
1. Browser sends request with relevant parameters to Server  
  - ebay.com/Products/10 where ebay.com is the address of Server and Products/10 are relevant parameters.  
2. Wait for Handler response  
  - HTML, files, etc., eg. index.html  
3. Browser does what it can, but will make more requests as needed   
  - Eg. when encountering \<img>, \<script>, etc. in index.html.

#### REST: REpresentational State Transfer
1. RESTful:
  - Representation State Transfer
  - URI (class of links, larger than URLs, more generic than URLs) – Resources → URL: Create Read Update Destroy

#### RESTful services:
  -On any particular URL, apply HTTP resources to it
    - GET: Read back user
      - Current state of resource
      - /users: representation of all users
      - /users/{id}: particular user
    - POST: Create new user
      - Data that helps to create user
    - PUT: Update user
    - DELETE: Destroy user

**REST Example:**
```
Resource: /users (all) or /users/id (specific)
Operations on /users:

GET    - Read           (Return current state)
POST   - Create {DATA}  (Create user with appropriate data)
PUT    - Update         (Update existing user)
DELETE - Destroy        (Delete user)
```

**Considerations when designing service:**  
 1. What database type?  
 2. How to handle new contact ids?  
 3. What inputs are acceptable?  
 4. How to format outputs?  
 5. How to implement error handling?

---
## Lecture 3 (1/20/2015)
#### RESTFUL WEB SERVICES
  - REST is an architectural style for web services
    - Invented by Roy Fielding at UC Irvine
  - REST is an approach to developing web services that mimics the design of the Web itself
  - Your service provides access to a linked set of resources
  - For each resource, you can perform operations on it similar to the main operations (aka methods) of the HTTP specifications

- REST Operations
  - For each resource, you can typically perform at least one of the CRUS (Create, Read, Update, Delete) operations
    - POST → CREATE a resource
    - GET → READ (i.e. retrieve) a resource
    - PUT → UPDATE a resource
    - DELETE → DESTROY a resource

Example REST resources:
```
GET /api/1.0/users
GET /api/1.0/users/0
POST /api/1.0/users
PUT /api/1.0/users/0
DELETE /api/1.0/users/0
GET /api/1.0/search?q=tattersail
```

- Operations cont.
  - Each operation may produce a result
    - With RESTful services, JSON format is king
  - POST and PUT methods typically send data
    - Also in JSON format
    - Maybe in the URL or in the body of the HTTP Request
      - For GET, the data may appear as query params
  - Other formats are possible: HTML & XML are typical
  - If a request needs to be authenticated
    - The authentication data appears in HTTP headers

- Issues
  - Security: how do you authenticate users?
  - Identity: how are ids assigned to resources?
  - Failure: how do we handle failure situations?
    - Most services user a combination of both JSON and HTTP Status Codes
  - Persistence: how are the resources stored?

---
## Lecture 4 (1/22/2015)
#### Git Presentation

###### Workflow
* Untracked
* Unmodified
* Staged
* Remote

Conflict best practice: Pull, Merge, Pull, Push

###### Initialization
Does the background work to start a git repository in the current directory.
```
git init
```

Creates a new git repo in current dir that is copy of remote repo
```
git clone <remote_repository_addresss>
```

###### Branching
```
git branch
git branch <new_branch_name>
```

To delete
```
git branch -d <new_branch_name>
```

```
git checkout <branch_name>
git checkout <commit>
```

###### Add and Commit
```
git add <file>
git commit -m "Commit Message"
```

###### Merging

Merges the name branch into the current branch.
```
git merge <branch_name>
```

###### How to Resolve Conflicts

1. open file with conflict
2. find the conflict
3. remove the markers and choose the lines of code which should not be the result of the merge
4. save the file
5. repeat from 1 until there are no more conflicts
6. add and commit the results of the merge

###### Push and Pull

Params are optional if the defaults are set
```
git pull <remote_repo> <branch_name>
```

Pushes all updated branches to their equivalent in the remote repo
```
git push <remote_repo>
```

###### Status

File statuses: untracked, unmodified, modified, staged
-b provides name for current branch
```
git status -b
```

###### Non-tracked files

Handled with .gitignore.  More than one can be used in single repo.  Removeds unwanted files from being marked as untracked.  See formatting for .gitignore.

###### Other useful commands

```
log - history of commits
remote - setup remote knowledge of remote repos
stash - similar to shelving in other VCS
rebase - method for changing how branches are related
diff - show differences between two states of the repo
fetch - gets changes, but does not integrate into local repo
reset - move about current head
tag - mark git objects
mv - move a files location within a repo
rm - stop tracking the changes to a file
```

#### Github Presentation

1. Create branch
2. Add some commits
3. Open a pull request (can use '@mention')
4. Discuss if good
5. Merge back into production

A fork is an exact copy of the repository. Splitting the project. You don't need collaborator access. If you have collaborator access, you can just branch.

Note: Master is always deployable to production.

Emoji - :thumbsup: or :shipit:

Can also use keywords.

---
## Lecture 5 (1/27/2015)
#### Node.js

Serverside tool and framework for executing Google's V8 javascript engine.

###### Explanation 1
Helloworld via HTTP
```javascript
// Load the http module to create an http server.
var http = require('http');

// Configure our HTTP server to respond with Hello World to all requests.
var server = http.createServer(function (request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello World\n");
});

// Listen on port 8000, IP defaults to 127.0.0.1
server.listen(8000);

// Put a friendly message on the terminal
console.log("Server running at http://127.0.0.1:8000/");
```

* Most code in node is packaged inside of a module. 
* HTTP is a core module, provided by Node.js itself. 
* npm package manager

###### Explanation 2
http provides function called createServer(), which returns an object with a method listen().
```javascript
http.createSserver(<function>).listen(1337, '127.0.0.1');
```

###### Explanation 3
anonymous function passed to function
```javascript
function(req, res){
  res.writeHead(200, {'Content-Type':'text/plain'});
  res.end('Hello World\n');
}
```

###### Explanation 4
```javascript
console.log('Server running at http://127.0.0.1/1337);
```

###### Explanation 5
All of this is executed immediately when passed to node.  If no future work remained, node would shut down.  This particular program will run forever because of event to check for new requests on every cycle of the event loop.
```
1. Get the http module
2. Create a server; register a function; start a server
3. Print out a message
```

##### Event Loops
Can add work to the event queue.

Functions that you can add to the queue for later execution
```javascript
process.nextTick()
setImmediate()
setTimeout()
setInterval()
```

A simple example using process.nextTick()
```javascript
consol.log("first!");
process.nextTick(function(){
  console.log("third!");
  });
console.log("second!");
```

* Our program would be the same if you replaced _process.nextTick()_ with _setImmediate()_
* They both schedule a funtion for the next iteration of the event loop
  * However, _setImmediate()_ allows IO-related callbacks to process first.
  * _process.nextTick()_ will prioritize your function, possibly causing IO starvation
* _setTimeout()_ takes a second parameter that specifies how long to wait before the function is executed
* _setInterval()_ takes a second parameter that specifies the interval at which this function should be executed

Node is ideal for event-style programming.

###### Callback hell
Callbacks are great for asynchronous programming, but *Callback hell* happens where callbacks get indented.  Each callback has a delay.

Occurs when you chain multiple asynchronous calls together.  To solve:
1. Use synchronous functions instead (discouraged because can cause blocking)
2. Use named callback functions
3. 

Example of closure:
```javascript
var multiple = function(multiple){
  reutrn function(num){
    return num * multiple;
  };
};
var byThree = multiple(3);
var byFour = multiple(4);
console.log("byThree(3): %d", byThree(3));
console.log("byFour(4): %d", byFour(4));
```

##### Node Exectution Model
* Node is single threaded for user-written code
* Any code that you write is guaranteed to be syncrhonous
* You do not have to worry about race conditions
* IO is handeled in parallel
* If you issue an asynchronous call for IO
  * your callback is registered
  * the IO call is executed in a separate thread
  * other events on the event loop are handled as normal
  * at some point, the IO completes and your callback is invoked

##### Curl Example
```
//GET Requests
curl http://epic-research.cs.colorado.edu:8080/api/1.0/methods
curl http://epic-research.cs.colorado.edu:8080/api/1.0/first
curl http://epic-research.cs.colorado.edu:8080/api/1.0/second
curl http://epic-research.cs.colorado.edu:8080/api/1.0/third

//POST Request
curl -X POST --data '{"value":1000, "author":"Ken"}' http://epic-research.cs.colorado.edu:8080/api/1.0/answer
```
---

## Lecture 6 (1/29/2015)

#### Express
* web application framework wrtitten in javascript for use in Node.js
* design was influenced by Sinatra
* makes it easy to define the endpoints of your web-based service
* has features (such as serving statif files) that allow you to creat a website
* minimal framework; designed to be augemnted by node packages that are then wired in as middleware

Example
```
mkdir express_test
cd express_test/
npm init
npm install --save express
npm install --save body-parser
npm install --save morgan
npm list
```

Can use "-g" to install globally instead of locally for webapp.

Example test.js
```javascript
var express = require('express');
var parser = require('body-parser');
var logger = require('morgan');

var time = require('./lib/time.js');

var app = express();

app.set('port', process.env.PORT || 3000);
app.set('env', process.env.NODE_ENV || 'development');

app.use(parser.json());

app.use(logger('dev'));

app.get('/api/1.0/current_time', function(req, res){
	res.json({status:true, time: time.current_tim()});
});

app.post('/api/1.0/from_now', function(req, res){
	res.json({status:true, data:time.from_now(req.body.date)});
});

app.listen(app.get('port'), function(){
	var message = 'Express started on http://localhost:';
	console.log(message + app.get('port'));
	message = 'Express is executing in the ';
	console.log(message + app.get('env') + ' environment');
});
```

Example time.js
```javascript
var moment = require('moment');

var current_time = function(){
	return moment().format('LL; LTS');
}

var from_now = function(date){
	return moment(date, 'YYY-MM-DD').fromNow();
}

exports.current_time = current_time;
exports.from_now = from_now;
```

curl command
```
$ curl -X POST --data '{"date":"2012-01-25"}' --header "Content-Type: application/json" http://localhost:3000/api/1.0/from_now
```

For Postman, set header Content-Type to application/json and put {"date":"2012-01-25"} in form data.

---

## Lecture 7 (2/3/2015)

#### AngularJS
Open source web application framework.  Powerful, but complicated.

##### Core Concepts
* Data Bindings - the value of an HTML tag can be associated with a model object.  When one changes, Angular updates the other automatically.
* Controllers - associated with a portion of your HTML and define all of the state and methods that can be accessed within that section of the page.  Allows you to _modularize_ your web apps. Manages data for some portion of a page while it is being displayed.
* Services - Allows you to maintain state between invocations of a controller or if you need to share state between two different controllers. Created when Angular app is initialized and will remain in place for lifetime of the application.
* Directives - ubiquitous, allows Angular to integrate into HTML in natural way. Can also create reusable components that combine controllers, data, and HTML.  For example, you can create a _login form_ component that can be re-used across multiple projects.
* Embeddable - Can control as much or as little of a web page as you specify.  It's easy to embed a small Angular component into an existing page and tehn incrementally add enw functionality over time.
* Injectable - _Dependency injection_  allows you to inject objects into a class, rather than relying on the class to create the object itself (e.g. factory design pattern, Spring).  Angular declares depndencies up front instead of using a main routine.  At run-tim, it will locate dependencies and inject them.

Entire MVC being essentially created in browser.

##### Modules
A module is the parimary way to package up a set of controllers into an Angular app.

Second parameter indicates that Angular needs to create it.  This has no dependencies.
```javascript
angular.module('contactsApp', [])
```

Once created, you can gain handle with no dependencies
```javascript
angular.module('contactsApp')
```

To narrow scope
```javascript
<html ng-app="contactsApp">
</html>
```

```javascript
angular.module('contactsApp').controller('MainController', [<dependencies and code>])
```

Simple controller with no dependencies.  Aliasing "this" creates closure.
```javascript
<MODULE>.controller('MainController', [function(){
	var self = this;
	self.name = "ken";
	self.update = function(){
		self.name = "Kenneth";
	};
}]);
```

## Lecture 8

#### Angular Demonstration

Angular runs in web browser.  Node is platform for web server.  Express builds on top of Node.

Rails is middleware.  E.g., Apache can hand-off to rails.

## Lecture 9

#### Implicit Binding

When a function is called as a method on an object. A function in this context is able to change the values of that object's properties via this.

```javascript
// Example 3
var increment = function() {
  this.age = this.age + 5;
};

var person1 = {
  age: 42,
  makeMeOlder: increment
};

var person2 = {
  age: 23,
  makeMeOlder: increment
};

person1.makeMeOlder();
person2.makeMeOlder();

console.log(person1.age); // prints 47
console.log(person2.age); // prints 28
```

#### Explicit Binding

When the execution context for a function is selected ahead of time and then used when that function is called, using bind(), call(), and apply().

```javascript
// Example 4
var increment = function(delta) {
  this.age = this.age + delta;
};

var person = {
  age: 42
}

increment.call( person, 5 ); // or increment.apply( person, [5] );

console.log( person.age ); // prints 47
```

#### Angular Continued

#### IIFES

JavaScript design pattern which produces a lexical scope using JavaScript's function scoping. Immediately-invoked function expressions can be used to avoid variable hoisting from within blocks, protect against polluting the global environment and simultaneously allow public access to methods while retaining privacy for variables defined within the function. This pattern has been referred to as a self-executing anonymous function. -Wikipedia

A common way to express this is to enclose both the function expression and invocation in parentheses.
```javascript
(function(){
  /* code */ 
}());
 
// And that's the way if some parameters shall be passed
(function(a, b){
  /* code */ 
})(arg1, arg2); //arg1 -> a; arg2 -> b
```
### Getting data from twitter

* Reactivate twitter account
* Checkout twitter developer site
	* Bottom right > manage your apps

***
## Lecture 10

* Consumer keys, Access tokens
	* Access to Twitter’s APIs are secured by OAuth
		* OAuth is a Web-based service inceptions with users and applications
	* With Twitters a consumer key identifies a particular app/developer
	* Allows an application to act on behalf of many users
		* you might ship you app with its consumer keys but with no access tokens. 
		* Then when you launch the app, it allows the user to sign into your twitter account.
			* Twitter will then send an access token/secret for you application to store on behalf of the user. 
	* We circumvent the account long in step by creating access token on the developer app creation
* Install **rbenv** and **ruby-build**
* Review lecture notes to run get_tweets
* Twitter requires we sign every request with an Authorization header

***
## Lecture 11

### Class Hierarchy 

* Twitter Request
	* RateLimits
	* Max Id Request
		* Timeline
		* Search Api
	* Streaming Twitter Request
		* Filter Track Stream
		* Public Strema
	* Cursor Request
		* Friends Id
		* Follower Id

***

* Contracts are created using interfaces in statically-typed lungs such as java
* In dynamically-typed languages like ruby fail fast

### Param and Props

* Added Features
	* Ability to control if a parameter is included in a reduces 
	* Ability to display parameter that are being sent in a request

### Logging

* Logging helper is used to create a default logger
	* Created in TwitterRequest’s constructor
	* Accessed using the log attribute

### Rates

* Helper invokes a twitter endpoint to get the app’s current set of rate limits
	* Limits stored in a class variable to be shared across all TwitterRequest instances

### Requests

* MaxIdRequest
	* Subclass for endpoints that need to traverse timelines with max_id parameters
* CursorRequest
	* Similar to MaxId however it does not need to define a contract for subclasses
	* Can implement all required functionality directly

### Timeline

Loops until all tweets are accessed or 16 request are successful

### Search 

Loop until we see zero tweets returned 

### Streaming Twitter Request

* Collect method is designed to run forever
* Create event handlers on streaming request 
	* on_headers: Response has started to stream back to us
	* on_body: Some data has been received from the server to process	
	* on_complete: Response has finished, can be used to determine to close connection
* Client Side
	* Can call request shutdown method
### Homework 3 Available

***
## Lecture 12

Homework 3 now available

### Document Database

Resources: 

* “Big Data: Principles and best practices of scalable realtime data systems”
* “Making Sense of NoSQL: A guide for managers and the rest of us”

#### Scaling with Traditional Databases

Example:

* “Imagine you’ve been asked to build a system that keeps track of page views on particular URLS
* Figure: Traditional Table
* Leads to issues when your application gets popular
	* Solution add a queue between your web server and the database code
	* Not a true solution
		* Adding workers to paralyze the queue doesn’t work because the database is the bottleneck
* Solutions:
	* Vertical Scaling:
		* Short term solution:
			* New Equipment - High Cost
			* Implement Cache in-between database and server, only allow writes to database. All reads hit queue
	* Shard the database:
		* Multiple copies of the database
			* Create several instances of the database. (Most likely on separate machines
			* Partition data across those databases
				* Develop a partition strategy, perhaps MD5 hash some aspect of the input data and then mod that value by the number of shards. 
				* Write the data indicated shard
* Not great solution due to shard failure and added application complexity
	* Fault tolerance is hard
	* Complexity is pushed to the application layer

#### NoSQL

* NoSQL databases are ones which are aware of their distributed nature
	* The manage sharing and replication
	* They are horizontally scalable
		* If you need more disk space, add a server
		* If you need computation to go faster, add a server
* Avoid mutable data
	* If a value changes you write a new immutable copy of the updated data
* Fault tolerant

#### Types of NoSQL Databases

* Key-Value
	* Database Hash Table
	* Values are un-typed
	* Simple
* Graphs
	* Databases optimized to store graph structures
	* Provide structural query languages
	* Efficiently traverse graphs
	* Shortest path between nodes
* Columnar
	* Column Family Stores
	* Able to scale to enormous amounts of data
	* Able to achieve fast writes
		* While still maintaining reasonable read performance
	* Netflix uses Cassandra to store and serve movies 
	* Column families can think of as a table
		* Consists of rows that have unique row keys
			* Rows consist of columns
				* Columns consist of a key and a value pair
	* Essentially hash tables all the way down
	* Grouped Rows on disk
* Documents
	* Similar to key-value with a little more structure
	* You enter documents (a bag of key-value pairs)

**Why NoSQL?** 
There is no schema. 
There is nothing that says: in column 5 of table 2, you will find an int: in column 6, you’ll find a VARCHAR, etc. 
You are often free to store anything in one of these databases
* Examples:
	* Document Stores:	
		* Each document can have a different set of key value pairs (name, location, birthday), (pet, bird, age)
	* Columnar Store: each row in a columnar store can have different columns 

***
## Lecture 13

### CouchDB

* Document NoSQL Database
	* Stores documents
	* Each document contains everything that might be needed by an app
	* No schema is enforced: each document can have different attributes
		* Allows for natural modeling of domains
* Written in Erlang
	* Built in support for concurrency
	* Built in fault 
* Design braces the web
	* RESTful API
	* Built for Distribution
* CAP Theorem: **(Pick any two)**
	* **Consistency**: All clients see the same data even in the presence of concurrent updates
	* **Availability**: All clients are able to read or write the data store when they want
	* **Partition Tolerance**: A database can be split across multiple servers
* CouchDB chooses: **Availability and Partition Tolerance**

#### CouchDB Internal:

* B-Tree storage engine
	* Automatic sorting; Allows searches, insertions, and deletions to occur in ```O(lg)```
* Employs MapReduce over this B-Tree to compute views of the data; allows for parallel and incremental computation
* No Locking
* Validation: Validation functions can be written in JS for a particular class of documents
	* Safeguard against malicious data 
* Incremental Replication
* Merge Conflicts

***
## Lecture 14

### MongoDB

* Indexes: B-Trees
* CAP Theorem:
	* Consistency
	* Availability
* Documents order hierarchically  
* Type and Case Sensitive

***
## Lecture 16

### MongoDB Indexes

* Use mongo Ruby gem to access MongoDB
* Convert created_at from string to times object
	* ``` t = DateTime.parse(“Sun Feb 15 02:41:32 +0000 2015”)```
	* ``` return t.to_time.utc ```
* Coordinate fields: used for geospatial queries
* ```explain``` function will return information about how DB will process any given query
* Indexes are stored on collections, not databases

***
## Lecture 17

### More on Indexes

* Can greatly reduce the number of documents that need to be examined to satisfy a query
* Index Cardinality
	* Number of possible values for an indexed field
		* A field like **employment status** has low cardinality since it has two values yes/no
		* Where as **name** has high carnality
	* In general you only want indexes on high cardinality fields
* Compound indexes can be difficult
	* Example sort by : ```user.created_at``` (oldest to youngest); ```created_at``` (most recent tweet to oldest tweet)
	* Reverse sort is: ```db.tweets.find().sort({‘user.created_at’:-1,’create_at’:1})```
	* Enable different queries:
		* Point Queries: search for a single value, then traverse index (either direction)
		* Multi-Value Queries: search for a range of values
* Full-Text Indexes
	* Support for a full text search
	* Only one full-text index per collection
* Geospatial Indexes
	* Cartesian Index
	* Spherical Index: 2dsphere
		* GeoJSON format
			* Supports points, lines, and polygons

### Map Reduce

* Ability to create a new collection from an old collection
	* ```db.tweets.mapReduce(map, reduce, {out: "users”});```

***
## Lecture 18

***
### Apache Solr

* Lucene
	* High-performance text search engine library
	* Inverted index - store the keywords of the documents in the index
* CU FCQ - Example
	* Searches three tables
	* DB - 100,000 rows
	* Excel to DB
* Solr has a REST API
	* Runs as a server

***
### Redis

* Key Value Store “Data-structure server”
* Not a database replacement
* Use for fast real-time data applications

***
### Kafka

* How to process data coming in real time.
	* Distributed
	* Fault-tolerant
	* High-throughput	
	* Publish-subscribe
	* Message system
* Publish - Subscriber
* Kafka relies on ZooKeeper for distributed falt tolerance

***
## Lecture 19

### Kafka Demo
* Fake twitter data through a framework stack
* Output to a web client

### Memcached

* Distributed memory object caching system
* Large hash table
	* Keys up to 250 bytes
* Data is disposable
* Cluster is flat

### Document DB (On Azure)

* Schema-free
* Indexing database
	* Automatically index documents added to DB

***
## Lecture 20

### Neo4J

* Graph based database
	* NoSQL
	* Whiteboard Friendly
		* Easy visualization
	* Relationship Focused
		* Edges are most important
	* Java Based
		* Open Source
* Fast for associative data sets
* Typically implemented on a single server versus a cluster

### HBase

* Hadoop Database
	* Open source distributed column-oriented
* Provides big table capabilities on top of Hadoop
* Table schema defines only column families
* Each cell value of the table has a timestamp
	* Automated versioning
* Used for lot of incoming data
	* Large amount of client/request

***
## Lecture 21

### Riak

* Key-Value Store Database
* NoSQL
* No Master node
	* Every node is a Master & Slave
* Scaling: Value of key defines which node the key will be stored on
* Written in Erleng

### Cassandra

* Scaled NoSQL database
* Elastic scalability
* Always on architecture
* Fast linear-scale performance

### Indexing in Cassandra

* Insert rows similar to SQL
* Composite Columns w/ primary key
* Clustering column sorts the data
	* One or more partition keys
	* Zero or more clustering column
* Secondary Indexes	
	* Cassandra provides support to add indexes over column values

***
## Lecture 22

### Javascript Closures and Design Patterns

* Scope
	* Example
* Closure
* Module Design Pattern
* Inheritance vs Prototype
* this
	* new Name()
		* refers to object it returns
	* explicit
	* implicit
	* default

### Ruby on Rails

* Ruby
	* No default function overloading
	* Able to return multiple values
* Rails framework
	* Gem setup

### Flask

* Micro framework
* Written in Python
* Testing is made ease with Flaskr

***
## Lecture 23

***
### Hadoop
* MapReduce
* Master/Slave

***
### Spark
* Fast Data Sharing
* MapReduce+
* Cluster Wide Caching

***
### Apache Storm
* Stream Processing
* Guaranteed Message Processing

***
## Lecture 24

***
### React

* Released by Facebook
* Maintains a virtual DOM
* One-way state binding
* JSX
	* Creates javascript objects using html syntax


***
### Sinatra

***
### Flux

* Single directional data flow
* Built by Facebook to combat scalability of MVC

***
## Lecture 25

### Google Cloud Platform

* Support Python, Java, PHP and Go 
* Google handles shading, load balancing, traffic splitting, elasticity, ect . . .
* Use Google fiber between Data Centers
* Data transmitted and stored in encrypted form 
* Three tiers of Cloud Storage
* Cloud SQL
	* Pay per use

### Docker

* Open-source engine that automates deployment of apps into containers
* Fight against dependency discrepancy
* Containers
	* Created from images
	* Isolated environment

### Capistrano

* Automated Server Deployment
	* Uses Rake DSL for tasks
	* Written in Ruby
* Can create custom tasks 
* Automate task for pulling repo to server

***
## Lecture 26

### Turf

* GeoJSON
* More for analysis than visualization

### JavaSript InfoVis Toolkit

* Library to create interactive data visualization on the web
* Composeable:
	* Combine multiple visualization into one
* Data is stored in static JSON objects

### Flask

* BSD
* Very extendable
* Uses ```pip install flask```

***
## Lecture 27

### D3 

* select
* bind

### Leaflet

* Layering
* MultiPlatform
* Call maps

### Vega

### Epic

* Epic Collect (Data Storage)
	* Keyword Tweets
	* Context Tweets

***
## Lecture 28

### JavaScrip Async and Promises

* Event Loop
* Callback
* Promises
	* Chain

### Titan

### Amazon Web Services

### Epic
