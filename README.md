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
