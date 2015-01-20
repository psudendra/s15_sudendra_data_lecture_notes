# Lecture Notes for Data Engineering Spring 2015

## Lecture 1 (1/13/2015)
1.     Data
Engineering

a.     Social
Networks:

b.     Data
Analytics

                                              
i.     Sampling

                                            
ii.     Machine
Learning

1.     Can
we predict what customers are going to do in the future?

2.     Predict
random user’s behavior

c.     Storage

                                              
i.     NoSQL

                                            
ii.     Document
databases

                                           
iii.     Graph
databases

                                           
iv.     Key-value
storage

                                            
v.     Colomner
stores (not key-values)

d.     Big
data

                                              
i.     Data
collection & cleaning

                                            
ii.     How
to access it?

                                           
iii.     Has
to clean before it can be stored

e.     InfoViz

                                              
i.     Huge
data sets, how do you view them to the user?

1.     D3
(JS framework)

2.     Tablo

3.     R

2.     Data
Life Cycle

a.     Question,
Curating, Triage, Persistence à Collection à Clean up à
Storage à
Processing, Analysis à Query, utilize, act

                                              
i.     Triage:
prioritization

 

3.     Request
Response Cycle

a.     Web
browser à
web server (HTTP server) à handler

                                              
i.     Example:
ebay.com/product/10

                                            
ii.     GET
à
POST à
DELETE à
PUT

b.     Until
handler returns something, we’re stuck in request cycle

                                              
i.     Example:
any web page, no requests; index.html

c.     Amazon
Recommendations:

                                               i.     HTML
will take data and render it in memory

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
