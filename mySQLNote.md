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
  - `AS`: rename a column or table with an alias which will show up in the result and only exists for the duration of the query.
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
    - `UPDATE table-name
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
  const Person = mongoose.model('Person', personSchema);
  ```

  - CRUD operation

    - use [mongoose library api](https://mongoosejs.com/) to perform queries on the model to create/read/update/delete items

      - callback style vs promise style

        - conditions
        - update: for update only
        - [projection]
        - [option]
          - { new: true }: for update only
          - { upsert: true }: for update only
        - callback: for callback style only

      - Read:

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
  - Commands:
    - `db`: display current database
    - `use <database>`: switch database
    - `show dbs`: list the databases
    - `show collections`: list all the collections
    - `db.<collectionName>.CRUD`: perform CRUD operation on this collection

<br>

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
