# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Introduction to MongoDB  

## Learning Objectives

By the end of this lecture, students will be able to:

- Explain what MongoDB is and how it differs from traditional relational (SQL) databases.
- Understand core MongoDB concepts, including databases, collections, documents, and fields.
- Describe the role of MongoDB Atlas as a cloud-hosted database service.
- Use MongoDB Compass to connect to a MongoDB Atlas cluster and explore stored data.
- Interpret and use a MongoDB connection string securely and correctly.
- Create databases and collections in MongoDB through data insertion.
- Perform full CRUD operations (Create, Read, Update, Delete) using MongoDB queries.
- Write basic and filtered queries using comparison and logical operators.
- Update single and multiple documents using appropriate update operators.
- Delete documents safely and understand the impact of delete operations.
- Recognize the purpose of the `_id` field and how MongoDB uniquely identifies documents.
- Apply best practices when working with MongoDB in a learning and development environment.
- Understand how MongoDB integrates conceptually with Java applications built in IntelliJ IDEA.

---

## What is MongoDB?

MongoDB is a modern NoSQL database designed to store and manage data in a flexible, scalable, and efficient way. Instead of using tables and rows like traditional relational databases, MongoDB stores data as documents in a format similar to JSON, making it intuitive and easy to work with in real-world applications. This document-based approach allows developers to model data naturally, adapt to changing requirements, and build applications that can scale seamlessly as data grows.


## Key Characteristics of MongoDB

- **Document-Oriented Storage**  
  MongoDB stores data as documents using BSON (Binary JSON), which allows complex data structures such as nested objects and arrays to be stored naturally.

- **Schema Flexibility**  
  Collections do not require a fixed schema. Documents in the same collection can have different fields, making MongoDB ideal for applications with evolving data requirements.

- **High Scalability**  
  MongoDB is designed to scale horizontally using sharding, allowing data to be distributed across multiple servers as the application grows.

- **High Performance**  
  Fast read and write operations are achieved through efficient indexing and in-memory data processing.

- **Rich Query Language**  
  MongoDB provides a powerful query language that supports filtering, sorting, projections, aggregation, and complex queries.

- **Indexing Support**  
  Indexes can be created on any field to improve query performance, including compound and text indexes.

- **Built-in Replication**  
  MongoDB uses replica sets to provide high availability and automatic failover in case of server failure.

- **Cloud-Native with Atlas**  
  MongoDB Atlas offers a fully managed cloud database with automated backups, monitoring, and security features.

- **Easy Integration with Applications**  
  MongoDB integrates smoothly with modern programming languages and frameworks, including Java-based applications.

- **Developer-Friendly**  
  Its JSON-like data format, flexible schema, and powerful tools make MongoDB easy to learn and productive for developers.

---

## MongoDB Terminology

| SQL Concept | MongoDB Equivalent |
|------------|-------------------|
| Database   | Database          |
| Table      | Collection        |
| Row        | Document          |
| Column     | Field             |
| Primary Key (id)| `_id`             |

---

## Documents and Collections

![The hierarchy of collections and documents](./assets/document-collection-hierarchy.png)



### Document
A document is a single record stored as key-value pairs.

```json
{
  "name": "Saad",
  "age": 30,
  "email": "saad@email.com"
}
```

### Collection
A collection is a group of related documents.  
Documents inside a collection **do not need to have the same structure**.

---

## MongoDB Atlas Overview

MongoDB Atlas is a **cloud-based MongoDB service**. It allows you to:
- Host databases online
- Manage security and users
- Connect from applications and tools like MongoDB Compass

---

## MongoDB Compass

MongoDB Compass is a **GUI tool** used to:
- View databases and collections
- Insert, update, delete, and query documents
- Run MongoDB queries visually or manually

---

## Connection String

A connection string is a single line of text that contains:
- Database location
- Username
- Password
- Connection options

It allows applications and tools like Compass to communicate with MongoDB securely.

---

## CRUD Operations in MongoDB

CRUD represents the four fundamental actions performed on data in a database:

- **Create** – Add new data  
- **Read** – Retrieve existing data  
- **Update** – Modify existing data  
- **Delete** – Remove data  

In MongoDB, all CRUD operations are performed on **collections**.

### Create Operation
Create operations are used to add new documents to a collection.

####  Create One Document

```js
db.students.insertOne({ name: "Saad", age: 30 })
```

####  Create Multiple Documents
```
db.students.insertMany([
  { name: "Sara", age: 21, major: "IT" },
  { name: "Omar", age: 23, major: "Engineering" }
])
```

- If the collection does not exist, MongoDB creates it automatically.
- MongoDB automatically generates a unique _id for the document.

### Read Operation
READ operations are used to retrieve data from a MongoDB collection. MongoDB provides a flexible and powerful query system that allows you to fetch all documents, filter results, combine conditions, and compare values.

All READ operations are performed using the `find()` or `findOne()` methods.

#### Retrieve All Documents from a Collection
```js
db.students.find()
```
#### Find by Field Value
```
db.students.find({ major: "IT" })
```

#### Find One Document
```
db.students.findOne({ name: "Ali" })
```
- Returns the first document that matches the filter.
- Useful when you expect a single result.

#### Find by _id
```
db.students.find({ _id: ObjectId("64f2a1b8c9edfdfbdfbdfdfv4") })

```

- Used to retrieve a specific document by its unique identifier.
- _id values must be of type ObjectId.

### Comparison Operators

Comparison operators allow filtering based on numeric or date values.

#### Greater Than ($gt)
```
db.students.find({ age: { $gt: 21 } })
```

#### Less Than ($lt)
```
db.students.find({ age: { $lt: 25 } })
```


#### Greater Than or Equal ($gte)
```
db.students.find({ age: { $gte: 18 } })
```

#### Less Than or Equal ($lte)
```
db.students.find({ age: { $lte: 30 } })
```

#### Not Equal ($ne)
```
db.students.find({ major: { $ne: "IT" } })
```


### Logical Operators

Logical operators combine multiple conditions.

#### AND Operator ($and)
```
db.students.find({
  $and: [
    { age: { $gt: 20 } },
    { major: "IT" }
  ]
})

```

- Returns students older than 20 AND enrolled in IT.
- Note: MongoDB also supports implicit AND:

```
db.students.find({ age: { $gt: 20 }, major: "IT" })
```

#### OR Operator ($or)
```
db.students.find({
  $or: [
    { major: "IT" },
    { major: "Engineering" }
  ]
})

```
- Returns students who are in IT OR Engineering.

#### NOT Operator ($not)
```
db.students.find({
  age: { $not: { $gt: 25 } }
})
```
- Returns students whose age is NOT greater than 25.








### Update Operation
```js
db.students.updateOne({ name: "Ali" }, { $set: { age: 23 } })
```



### Delete Operation
```js
db.students.deleteOne({ name: "Ali" })
```

---

## Summary

- MongoDB is a NoSQL, document-oriented database designed for flexibility and scalability
- Data is stored as documents within collections rather than tables and rows
- MongoDB Atlas provides a cloud-based platform for hosting and managing databases
- MongoDB Compass offers a graphical interface to explore, query, and manage data visually
- Databases and collections are created automatically when data is first inserted
- Each document contains a unique `_id` field for identification
- CRUD operations (Create, Read, Update, Delete) enable full control over database data
- MongoDB supports powerful query features such as filtering, sorting, and logical operators
- The flexible schema allows data structures to evolve with application requirements
- MongoDB integrates well with Java applications developed using IntelliJ IDEA
