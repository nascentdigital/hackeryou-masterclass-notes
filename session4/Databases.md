# Database Design

<br/>

## Relational vs Non-Relational

### Relational (SQL Server, MySQL, PostgreSQL, SQLite, Oracle DB, IBM Db2)
Pros:
- They implicitly document the structure and intention of the data
- They support strong relationships between data entities 
- They support strong validation rules
- They are portable and decoupled from any application logic
- The patterns for structuring data is very simple

Cons:
- There is quite a bit of setup before you can use it
- - Schemas are rigid. Databases, tables, columns, and relationships need to be created before you can begin to use it.
- Changes to structure often require data migration (not simple)

### Schemaless (MongoDB, CouchDB, DynamoDB, Cassandra)
Pros:
- You can jump in immediately and start using them without any setup
- - Can begin with an empty instance and create the schema on the fly as needed in code
- You can change the data as you application and deal with migration later
- You can usually create complex data structures (Document Store vs Wide Column)
- The query languages tend to be much more powerful

Cons:
- Governance of data is left up to the applications
- It is very easy to create poor data structures that don't scale

### Considerations
- How stable is the data design and structure?  Are you prototyping?  Is it likely to change?
- Are there many complex relationships to be fetched (e.g. many-to-many)
- Is the data being accessed by multiple applications or services?
- How many fields will the records have?

<br/>


## Document Database Best Practices

### Relationships

Although a document database doesn't technically support relationships between entities,
you still will have them in your applications.  Many of the problems that developer run into
start with poor design of their relationships.


##### Embedded Document (one-to-few)

Consider a collection of projects, where each team has a list of developers:  
```json
{
    "_id" : ObjectId("50f1e2c99beb36a0f45c6453"),
    "project": "Brightmind iOS",
    "client": "90f49ad6444c11ac2448a5d6",
    "team": [
        {
            "_id": 45,
            "name": "Linda",
            "role": "Product Designer"
        },
        {
            "_id": 12,
            "name": "Braini",
            "role": "Architect"
        },
        {
            "_id": 78,
            "name": "Sofia",
            "role": "Team Lead"
        },
        {
            "_id": 2,
            "name": "Simeon",
            "role": "Developer"
        }
    ]
}
```


##### Embedded Reference (one-to-many or many-to-many)

The previous scenario works because the scale of embedded data is small, but this approach
breaks down when the children / subdocuments:
 - Scale up in volume 
 - Become large in size (e.g. a team member has lot of data)
 - Are referenced by multiple documents (e.g. team members can be on multiple projects)
 - Live longer than the parent (e.g. person doesn't get fired after a project)

Consider the approach of an embedded reference, where the team members are moved to 
another collection:
```json
{
    "_id" : ObjectId("50f1e2c99beb36a0f45c6453"),
    "project": "Brightmind iOS",
    "client": "90f49ad6444c11ac2448a5d6",
    "team": [ 45, 12, 78, 2 ]
}
```

##### Parent Reference (one-to-lots)

This is a lot better, but we can still run into situations where that list of children
scales up to a very large size.  In that case you need to inverse the relationship and 
have the **child entity** reference the parent.

Consider a collection of log entries that google might put against a server:

###### db.getCollection('server')
```json
{
    "_id" : ObjectId("88f1e2c99beb36a0f45c6453"),
    "address": "203.103.66.43",
    "name": "Amadeus"
}
```

###### db.getCollection('server_logs')
```json
{
    "_id" : ObjectId("10f1e2c99beb36a0f45c6453"),
    "server": "88f1e2c99beb36a0f45c6453",
    "message": "Message 1"
}

{
    "_id" : ObjectId("10f1e2c99beb36a0f45c6454"),
    "server": "88f1e2c99beb36a0f45c6453",
    "message": "Message 2"
}

{
    "_id" : ObjectId("10f1e2c99beb36a0f45c6455"),
    "server": "88f1e2c99beb36a0f45c6453",
    "message": "Message 3"
}
```

How would we model an externalized child where there was more than one parent?


### Indexes

Indexes are the most often missed design step when building a production database.  They are 
very simple to create in MongoDB:

```js
db.restaurants.createIndex({ cuisine: 1 })

db.getCollection('restaurants')
    .find({ cuisine: 'Italian'})
```

We can also create a compound index that allows us to query across multiple fields:

```js
db.restaurants.createIndex({ name: 1, cuisine: 1, borough: 1 })

db.getCollection('restaurants')
    .find({ cuisine: 'Italian'}, { _id: 0, name: 1})
    .sort({ name: 1})
```

##### Considerations
- Make sure you can fit your indexes in RAM
    - Indexes will be loaded into memory if possible
    - Data will sit on disk in [BSON](https://www.mongodb.com/json-and-bson) format
    - If you indexes don't fit in memory the OS will have to fallback to swapping (REALLY SLOW!)
- Use them to speed up sorting
    - Otherwise the OS needs to sort afterwards
- Use compound indexes to create *covered queries* to make things faster
    - If all the data you project is indexed it doesn't need to reach into the BSON
- Debug using `explain()`

<br/>


### Transactions

In a traditional database you would normally make an update as follows:

1. Query to fetch the record frmo the database
2. Update the record in your code
3. Write the updated record back to the database

This can open up a concurrency problem.  What happens if two people start to update the
same record at the same time:

```js
[REQUEST 1] Reads data
                            Reads data   [REQUEST 2]
[REQUEST 1] Updates data
                            Updates data [REQUEST 2]
                            Writes data  [REQUEST 2]
[REQUEST 1] Writes data
```

In MongoDB you should never do that.  Use `findAndModify()` with supporting commands to 
support transactions.  

###### Incrementing within a transaction
```js
db.getCollection('restaurants')
    .findAndModify({
        query: { _id: ObjectId("5a319ad32266627b210a4e16") },
        update: { $inc: { reviews: 1 } },
        new: true
    })
```

There are also situations where data needs to be removed on demand.  In these cases a
`remove(query)` is one option, but sometimes the condition is time-based.  

##### Use TTL for Transactional Pruning
```js
db.getCollection('restaurants')
    .createIndex( { "createdAt": 1 }, { expireAfterSeconds: 5 } )
    
db.getCollection('restaurants')
    .insert({ name: 'test', createdAt: new Date() })
```
- Use TTL to handle time-sensitive data

<br/>


### Tweaking

- Pimp the `_id` field
- Field names cost you space
    - At scale this is not funny (1 character per million records results in MBs of space)
- Shard your data across tables or even databases for concurrency
    - Leverage hashes or custom partition keys

 
