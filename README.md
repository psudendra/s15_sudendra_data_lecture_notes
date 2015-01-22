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
  - RESTful:
    - Representation State Transfer
    - URI (class of links, larger than URLs, more generic than URLs) – Resources → URL: Create Read Update Destroy

  - RESTful services:
    - On any particular URL, apply HTTP resources to it
      - GET: Read back user
        - Current state of resource
          - /users: representation of all users
          - /users/{id}: particular user
      - POST: Create new user
        - Data that helps to create user
      - PUT: Update user
      - DELETE: Destroy user

---
## Lecture 3 (1/20/2015)
 - REST
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

- Examples
  - GET /api/1.0/users → Retrieve a list of all users
  - GET /api/1.0/users/0 → Retrieve the details of User 0
  - PUT /api/1.0/users/0 → Update User 0
  - GET /api/1.0/search?q=tattersail → perform a search with the query tattersail

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
