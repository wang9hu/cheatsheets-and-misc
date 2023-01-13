Popular Databases languages: Oracle, MySQL, MS SQL Server, **PostgreSQL**, **MongoDB**(NoSQL), etc

SQL: Structured Querry Language, a relational database

**Data stores**:

- tables(SQL)
- Documents(NoSQL)
- Key-Value(NoSQL)
  <br>

**Table Stores**: a relational database(SQL) is composed of tables

- has columns: cols don't change (attributes/fields) (defined as a schema)
  - primary key: unique id for each record
- has rows: rows are instances (records/tuplets), added continously
- can't have composite datatype in table, only string, nums, etc.
  <br>

**PostgreSQL**: relational database

- focus on extensibility and standards-compliance
- **ACID** compliant, supporting industry best practice
  <br>

**ACID**: **Atomicity** (all or nothing), **Consistency**, **Isolation** (concurrency control), and **Durability**, a set of principles that ensure database transactions are processed reliably

- SQL is ACID compliant
- noSQL is **not** ACID compliant
  <br>

**schemas**: enforced structure in data store

- in SQL: (required) defines the cols and rows that data must follow
- in NoSQL: not used in key-value, optional in Document
  <br>

**ER diagram**: entity relationship diagram
<br>

**Document Stores**: close to JSON (NoSQL)

- like a JS object
- also has unique id, auto generated or manually set
- collections of documents/composite datatype
- have ability to nest arbitrarily deep (has pros and cons)
- not ACID compliant, focus on **speed**
  <br>

**NoSQL**: increasingly used in big data and real-time web app

- simplicity of design, simpler horizontal scaling of clusters of machines, and finer control over availability
- "faster" and "more flexible"

<br>

**MongoDB** from humongous (NoSQL)

- ad hoc queries: support field, range queries, and regex
- indexing: any field can be indexed
- replication: store data as two or more copies
- load balancing: scales horizontally using sharding
- aggregation: MapReduce can be used for batch processing of data and aggregation operations
  <br>

**Key-Value store** (NoSQL)

- without nesting: Redis, Riak, LocalStorage
  - **Redis** is an open-source data structure server
    - most popular key-value solution
    - holds entire dataset in RAM and syncs back to the disc per 2s
    - fast because data is memcached
    - a good choice if a highly scalable data store shared by multiple processess or multiple apps are required
- don't use it as main database
- not very reliable
  <br>

**Relationships**:

- **Relational DB** (SQL):
  - **one to one** vs **one to many** vs **many to many**: they are handled differently
  - Foreign keys: in one table set up a field as foreign keys, which refers another field (mostly primary key) in another table
  - join table: consisit of foreigh keys
- **Document Store** (NoSQL):
  - Nesting vs Referencing: fastest vs robust
    <br>

**Security Vulnerablilitie**:

- mass assignment:
  - solution: Be Explicit --- Denylist / Allowlist

---

### SQL syntax:

- **CRUD**:

  - create: INSERT
  - read: SELECT
  - update: UPDATE
  - delete: DELETE

- **Syntax**:

  - `=` : equal
  - `!=` : not equal
  - `<>` : strictly not equal
  - `>` / `<`: larger / smaller
  - `*`: everything
  - `E%`: begins with `E`
  - `E___ %`: four letter long and begins with `E`
  - ...

- **Queries**:

  - `table-name.col-name`: get col from table
  - `AND`:
  - `OR`:
  - `NOT`:
  - `AS`: rename a column or table with an alias which will show up in the result and only exists for the duration of the query. ( [SQL Alias](https://www.sqltutorial.org/sql-alias/) )
    <br>
  - join tables: set up search area
    - `INNER JOIN`: only overlapping part of two tables
    - `LEFT OUTER JOIN`: all left table and overlapping part of right table
    - `RIGHT OUTER JOIN`: all right table and overlapping part of left table
    - `FULL OUTER JOIN`: all left and right tables
    - `ON`: condition of joined table
      <br>
  - read:
    - `SELECT` col-name
    - `FROM` table-name
    - `WHERE` condition
    - `LIKE` wildcards word
    - `NOT LIKE`: anything but...
    - `ORDER BY` sort-order
    - use `;` to end a query
  - create:
    - `INSERT INTO` table-name (col-name)
    - `VALUES` (col-valumes)
  - update:
    - `UPDATE` table-name
    - `SET` col-name `=` col-new-value
    - `WHERE` condition
  - delete:
    - `DELETE FROM` table-name
    - `WHERE` condition (must include `WHERE` or SQL will delete the entire table)
      <br>

- **Aggregate functions**:
  - `min(col)`: smallest value
  - `max(col)`: largest value
  - `sum(col)`: sum of the numeric values
  - `average(col)`: average value
  - `count(col)`: count values in a col
  - `count(*)`: count rows in a table
    ...
    <br>
- **Sub query**:
  e.g., `SELECT description FROM item_order WHERE price = (SELECT min(price) FROM item_order);`
  <br>

---

### Node-postgres

Install `npm install pg`
<br>
[psql APIs](https://node-postgres.com/):

- pg.Client
- pg.Pool
- pg.Result
- pg.Types
- Cursor
  <br>

---

### NoSQL

**MongoDB document store**

- **ODM**: object document mapping
  - everthing is store as BSON (Binary JSON)
  - instead of tables, data is stored in collections of documents
    - docuemnt is like Javascript object
    - can store **array** and **object** data types
    - can nest arbitrarily deep
  - emphasis on speed, but can only look up thing unidirectional, from top to nested
  - Not equipped to handle complex relationships as SQL
    <br>
- **Mongoose**: a MongoDB libary, provides structure to raw MongoDB, installed on server

  - enforces the use of schema: definitions and types
    - String, Number, Date, Array, ObjectId, Mixed(any type)...
    - Custom types: .....

  ```
  // create a model
  const mongoose = require('mongoose')
  const personSchema = new mongoose.Schema({
    name:{type: String, required: true},
    age: Number,
    quote: String,
    data: Mixed
  });
  ```

  <br>

  - mongoose will by default produces a collection name based on the pluralized name when setting the model

  ```
  // here passing 'person' when setting the mode, and its collection will be called 'people' (pluralized)
  const Person = mongoose.model('person', personSchema);
  ```

  - CRUD operation

    - use [mongoose library api](https://mongoosejs.com/) to perform queries on the model to create/read/update/delete items

      - **callback style** vs **promise style**

        - conditions
        - update: for update only
        - [projection]
        - [option]
          - { new: true }: for update only
          - { upsert: true }: for update only
        - callback: for callback style only

      - Read: (will return a query, use **promise style** or **callback style** to process the results)

        - Model.find
        - Model.findOne

      - Create:

        - Model.prototpye.save
        - Model.create (can also create an array of obj)

      - Delete:

        - Model.findOneAndDelete
        - Model.deletOne
        - Model.remove
        - Model.deleteMany

      - Update:

        - Model.findOneAndUpdate
        - Model.updateOne
        - Model.updateMany

    <br>

- **Mongosh**: the MongoDB Shell, a fully functional Javascript and Node.js REPL environment for interacting with MongoDB.

  - Commands ([Docs](https://www.mongodb.com/docs/mongodb-shell/reference/methods/)):

    - `cls`: clear screen
    - `exit`: exit mongosh
    - `db`: display current database
    - `use <database>`: switch to `<database>`, even if it doesn't exist
    - `show dbs`: list the databases
    - `show collections`: list all the collections
    - `db.dropDatabase()`: delete current database (when inside of target database)
    - `db.<collection>.CRUD`: perform CRUD operation on this collection

      - `db.<collection>.insertOne(<Object>)`: create one document
        - will add to `<collection>` of current database, will create database if not exist before
      - `db.<collection>.insertMany([<Object>, <Object>, <Object>, ...])`: create many documents
        <br>
      - `db.<collection>.find([...])`: return a \<cursor\>, which auto iterates up to 20 times to show the first 20 document
        - \<cursor\> has many methods that can be chained together, like `.sort()`, `.limit()`, `.skip()`, ...
      - `db.<collection>.find({ name: "Xiao" }, { age: 1 })`: returned all documents with `name` value of `"Xiao"` containing only the `age` and the `_id` (by default) of the document
      - `db.<collection>.find({ name: "Xiao" }, { _id: 0 })`: returned all documents with `name` value of `"Xiao"`containing everything but the `_id`
      - `db.<collection>.count({ name: "Xiao" }, { _id: 0 })`: returned the number of above documents
        <br>
      - `db.<collection>.updateOne({ name: "Xiao" }, { $set: { name: "Wang" } })`: update the document, change its `name` value
      - `db.<collection>.updateOne({ _id: ObjectId(".....") }, { $inc: { age: 3 } })`: update the document, increment `age` by 3
      - `db.<collection>.updateOne({ _id: ObjectId(".....") }, { $rename: { name: "firstName" } })`: update the document, rename its `name` to `firstName`
      - `db.<collection>.updateOne({ _id: ObjectId(".....") }, { $unset: { name: "" } })`: update the document, remove its `name` property
      - `db.<collection>.updateOne({ _id: ObjectId(".....") }, { $push: { hobbies: "cooking" } })`: update the first fit document, push `"cooking"` inside of `hobbies` value array
      - `db.<collection>.updateOne({ _id: ObjectId(".....") }, { $pull: { hobbies: "cooking" } })`: update the first fit document, remove `"cooking"` from `hobbies` value array
      - `db.<collection>.updateMany({ address: { $exist: true }}, { $unset: { address: "" } })`: update all document that has `address` key and remove `address` property
        <br>
      - `db.<collection>.replaceOne({ name: "Xiao"}, { age: 33 })`: replace the first fit document entirely with `{ age: 33 }`(don't use normally)
        <br>
      - `db.<collection>.deleteOne({ name: "Xiao"})`: delete the first fit document entirely
      - `db.<collection>.deleteMany({ name: "Xiao"})`: delete all documents that fits entirely
        <br>

        ...

<br>

- Also can use [aggregation Operations](https://www.mongodb.com/docs/manual/aggregation/) to process multiple documents and return computed results.
  - `$eq`: `db.<collection>.find({name: { $eq: "Xiao" }})`: return all documents with `name` is `"Xiao"`
  - `$ne`: `db.<collection>.find({name: { $ne: "Xiao" }})`: return all documents with `name` is not `"Xiao"`
  - `$in`: `db.<collection>.find({name: { $in: ["Xiao", "Wang"] }})`: return all documents with `name` is either `"Xiao"` or `"Wang"`
  - `$nin`: `db.<collection>.find({name: { $nin: ["Xiao", "Wang"] }})`: return all documents with `name` is neither `"Xiao"` nor `"Wang"`
  - `$exist`: `db.<collection>.find({age: { $exist: true }})`: return all documents that have `age` key
  - `$exist`: `db.<collection>.find({age: { $exist: false }})`: return all documents that do not have `age` key
  - `$gt / $lt`: `db.<collection>.find({age: { $gt: 20, $lt: 40 }})`: return all documents whose `age` key have value between 20 and 40 (exclusively)
  - `$gte / $lte`: `db.<collection>.find({age: { $gte: 20, $lte: 40 }})`: return all documents whose `age` key have value between 20 and 40 (inclusively)
  - `$or`: `db.<collection>.find($or: [{age: {$gte: 20}}, {name: "Xiao"}])`: return all documents that either has an `age` value that is greater than or equal to 20, or has a `name` value of `"Xiao"`
  - `$not`: `db.<collection>.find({ age: { $not : { $gte: 20 } } })`: return all documents that has `age` value that is smaller than 20 (not (greater than or equal to))
  - `$expr`: `db.<collection>.find({ $expr: { $gt : ["$apple", "$banana"] } })`: return all documents whose `apple` value is greater than `banana` value (`expr`: expression)
  - `<nested_property>`: `db.<collection>.find({ "address.street": "123 Main st" })`: return all documents whose `address` nested `street` value is `"123 Main st"`
    ...

( ==kill port after close vscode==: `npx kill-port 3000`)

- MongoDB vs SQL

---

### Data Modeling

- **Identify Entites**

- **Identify Relationships**
  - Barker's Notation:
    - 6 relationship mapping entities: one, many, one and only one, zero or one, one or many, zero or many
- **Identify Attributes**
- **Assign Keys**
- **Normalization** : 7 steps, don't always need to normalize.
  - first 3:
    1. There may be no repeating groups of columns in an entity
       - anytime when array is required, create a new table and establish a link via a one-to-many relationship.
    1. All attributes of an entity should be fully dependent on the whole Primary key.
    1. All attributes need to be directly dependent on the primary key, and not on the other attributes.
  - last 4: low level
