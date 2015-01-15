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
