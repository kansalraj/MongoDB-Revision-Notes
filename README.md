# MongoDB-Revision-Notes
<details>
<summary><b>Introduction to MongoDB</b></summary>
<br/>
   
MongoDB is a versatile, open-source, and cross-platform distributed document database. Developed by MongoDB Inc., it falls under the NoSQL database category, providing a dynamic approach to data storage and retrieval.

1. **Ease of Use**:
   - MongoDB is document-oriented, unlike traditional relational databases.
   - Data is stored in documents, allowing flexible representation of complex relationships within a single record.
   - No predefined schemas required, enabling easy addition or removal of fields in documents.
   
2. **Designed for Scalability**:
   - Scalability is a crucial consideration as databases expand over time.
   - Two common scaling strategies:
     - Scaling up: Upgrading existing server with more resources, costly.
     - Scaling out: Adding more servers to the cluster, cost-effective but complex management.
   - MongoDB is inherently built for scaling out.
   - Data can be distributed across multiple servers.
   - Automatic load balancing, data redistribution, and routing updates to the appropriate servers.
   - Sharding used for distributing data across multiple servers effectively.
   
3. **Rich Features**:
   - MongoDB offers standard database operations: insert, update, delete, and select data.
   - Additional features include:
     - Indexing: Enhances data retrieval speed.
     - Aggregation: Allows complex data analysis.
     - Collection and index type specifications: Tailors storage and retrieval options.
     - File Storage: Enables efficient handling of file-based data.
   - Comprehensive exploration of these features is covered in subsequent tutorials.

4. **High Performance**:
   - MongoDB emphasizes both architectural and feature-based performance.
   - The database philosophy prioritizes scalability, flexibility, and speed.
   - Aims to provide a robust, feature-rich database solution with exceptional performance.

In summary, MongoDB is a versatile NoSQL database that simplifies data storage through document-oriented architecture, excels in scalability by facilitating distributed data management, offers a range of features for advanced data manipulation, and maintains high performance through a comprehensive approach to architecture and features.
</details>


<details>
<summary><b>Basic Concepts of MongoDB: Documents, Collections, Databases, and Namespaces</b></summary>
<br/>
   
**Data Formats:**
- MongoDB uses JSON (JavaScript Object Notation) and BSON (Binary JSON) formats for data representation and storage.
- JSON is a structured data format based on JavaScript ECMA-262 3rd edition.
- BSON is a binary-coded serialization of JSON-like documents.

**JSON (JavaScript Object Notation):**
- JSON documents are collections of structured field-value pairs.
- Example JSON document:
  ```
  {
     "first_name": "John",
     "last_name": "Doe",
     "age": 22,
     "skills": ["Programming", "Databases", "API"]
  }
  ```

**BSON (Binary JSON):**
- BSON is a binary-encoded serialization of JSON documents.
- MongoDB stores data as BSON documents.

**Documents:**
- Documents are sets of field-and-value pairs.
- A document's structure: `{ field_name1: value1, field_name2: value2, ... }`
- Example:
  ```
  {
      _id: ObjectId("5f339953491024badf1138ec"),
      title: "MongoDB Tutorial",
      isbn: "978-4-7766-7944-8",
      published_date: new Date('June 01, 2020'),
      author: { first_name: "John", last_name: "Doe" }
  }
  ```

**Collections:**
- MongoDB stores documents in collections.
- Collections are analogous to tables in relational databases.
- Collections have a dynamic schema, allowing documents of varying structures.
- Example collections: "books," "users," etc.

**Databases:**
- MongoDB stores collections within databases.
- One MongoDB instance can host multiple databases.
- Databases are referenced by names (e.g., "bookdb").
- Database names should avoid reserved names and certain characters.

**Namespace:**
- A namespace is a combination of a database name and a collection name.
- It fully qualifies a collection within a database (e.g., "bookdb.books").

In summary, MongoDB utilizes JSON and BSON for data representation. Data is stored as documents in collections within databases. Namespaces allow for fully qualified collection referencing. Understanding these fundamental concepts is essential for effectively working with MongoDB's data storage and retrieval.

</details>


<details>
<summary><b>Commonly Used MongoDB Data Types</b></summary>
<br/>
   
1. **Null Type**:
   - Represents null or absence of a field.
   - Example: `{ "isbn": null }`

2. **Boolean Type**:
   - Has values `true` and `false`.
   - Example: `{ "best_seller": true }`

3. **Number Type**:
   - Default is 64-bit floating-point numbers.
   - Example: `{ "price": 9.95, "pages": 851 }`
   - Use `NumberInt` for 4-byte integers and `NumberLong` for 8-byte integers.

4. **String Type**:
   - Represents UTF-8 character strings.
   - Example: `{ "title": "MongDB Data Types" }`

5. **Date Type**:
   - Stores dates as 64-bit integers (milliseconds since Unix epoch).
   - Example: `{ "updated_at": new Date() }`
   - Use `Date` class in JavaScript, call `new Date()` for object.
   - MongoDB displays in local time, no time zone stored.

6. **Regular Expression Type**:
   - Stores JavaScript regular expressions.
   - Example: `{ "pattern": /\d+/ }`

7. **Array Type**:
   - Stores a list of values of any type.
   - Example: `{ "title": "MongoDB Array", "reviews": ["John", 3.5, "Jane", 5] }`

8. **Embedded Document Type**:
   - Allows a document as a value within another document.
   - Example:
     ```
     {
         "title": "MongoDB Tutorial",
         "pages": 945,
         "author": {
            "first_name": "John",
            "last_name": "Doe"
         }
     }
     ```

9. **Object ID Type**:
   - Unique identifier for documents.
   - Default for `_id` key, 12-byte value:
     - 4-byte timestamp (seconds since Unix epoch)
     - 5-byte random value
     - 3-byte increment counter
   - Generated globally unique IDs across servers.
   - Automatically generated if not specified.
   - Example output:
     ```
     {
         "acknowledged" : true,
         "insertedId" : ObjectId("5f2fcae09b58c38603442a4f")
     }
     ```
</details>

<details>
<summary><b>insertOne() insertMany() Method: </b></summary>
<br/>

**insertOne() Method:**

- **Purpose**: insertOne() method is used to insert a single document into a collection.
- **Syntax**:
  ```javascript
  db.collection.insertOne(
     <document>,
     { writeConcern: <document>}
  );
  ```
- **Parameters**:
  - `<document>`: The document you want to insert (required).
  - `writeConcern`: Optional argument for the level of acknowledgment.
- **Return**: The method returns a document with fields:
  - `acknowledged`: True if operation executed with write concern, false if not.
  - `insertedId`: Value of `_id` field of the inserted document.

- If collection doesn't exist, insertOne() creates it.
- If `_id` not specified, MongoDB generates a unique `_id` (ObjectId) for the document.
- If `_id` specified, it must be unique within the collection.

**insertMany() Method:**

- **Purpose**: insertMany() method inserts multiple documents into a collection.
- **Syntax**:
  ```javascript
  db.collection.insertMany(
     [document1, document2, ...],
     {
        writeConcern: <document>,
        ordered: <boolean>
     }
  );
  ```
- **Parameters**:
  - `[document1, document2, ...]`: Array of documents to be inserted.
  - `writeConcern`: Optional write concern.
  - `ordered`: Boolean indicating ordered/unordered insert.
- **Return**: Document with fields:
  - `acknowledged`: True if operation executed with write concern, false if not.
  - `insertedIds`: Array of `_id` values of inserted documents.

- Collection is created if not existing.
- If `_id` not specified, MongoDB generates unique `_id` (ObjectId).
- If ordered is true, inserts in order; if false, may reorder for performance.
- Throws BulkWriteError exception in case of error.
**If an error occurs, the ordered insert will stop while the unordered insert will continue to process for the remaining documents in the queue.**

</details>

<details>
<summary><b>findOne() find() Method & Projection </b></summary>
<br/>
   
## MongoDB findOne()

- `findOne()` retrieves a single document from a collection based on a specified condition.
- Syntax: `db.collection.findOne(query, projection)`
- `query`: Criteria for document selection.
- `projection`: Specifies fields to be returned.
- Omitting `query` returns the first document according to natural order.
- Default projection includes all fields.
- Use `{field: 1}` to include a field, `{field: 0}` to exclude.
- `_id` is included by default; exclude with `_id: 0`.
- If multiple documents match, first based on storage order is returned.

### Examples:

1. No arguments: `db.products.findOne()`
2. With filter: `db.products.findOne({_id: 2})`
3. Select fields: `db.products.findOne({_id: 5}, {name: 1})`

## MongoDB find()

- `find()` retrieves documents from a collection.
- Syntax: `db.collection.find(query, projection)`
- `query`: Selection criteria; `{}` returns all documents.
- `projection`: Fields to be returned.
- `_id` is included by default; exclude with `_id: false`.
- Returned as a cursor; automatically iterated in mongo shell.
- Use `it` command to continue iteration.

### Examples:

1. All documents: `db.books.find()`
2. Specific document: `db.books.find({_id: 10})`
3. Select fields: `db.books.find({categories: 'Java'}, {title: 1, isbn: 1})`


## Projection in MongoDB Queries

1. **Returning all fields in matching documents**:
   - `db.products.find({price: 899});`

2. **Returning specified fields including the `_id` field**:
   - `db.products.find({}, {name: 1, price: 1});`
   - To exclude `_id`, explicitly specify in projection:
     `db.products.find({}, {name: 1, price: 1, _id: 0});`

3. **Returning all fields except for some fields**:
   - Use projection to exclude fields:
     `db.products.find({_id:1}, {releaseDate: 0, spec: 0, storage: 0});`

4. **Returning fields in embedded documents**:
   - Include fields in embedded documents:
     `db.products.find({_id:1}, {name: 1, price: 1, "spec.screen": 1});`

   - In MongoDB 4.4+, specify embedded fields using nested form:
     `db.products.find({_id:1}, {name: 1, price: 1, spec : { screen: 1 }});`

5. **Projecting fields on embedded documents in an array**:
   - Project fields from embedded arrays:
     `db.products.find({}, {name: 1, "inventory.qty": 1});`

## Summary:

- Use `{<field>: 1}` to include the `<field>` and `{<field>: 0}` to exclude it.
- Use `{ <embeddedDocument>.<field>: 1}` to include `<field>` from `<embeddedDocument>`, and `{ <embeddedDocument>.<field>: 0}` to suppress it.
- Use `{ <arrayField>.<field>: 1}` to include `<field>` from embedded array, and `{ <arrayField>.<field>: 0}` to exclude it.

</details>

<details>
<summary><b>COMPARISON QUERY OPERATORS - $eq $lt $gt $gte $ne $in $nin</b></summary>
<br/>

**Introduction to the MongoDB $eq Operator:**

The `$eq` operator is a comparison query operator in MongoDB that allows you to match documents based on whether the value of a specified field is equal to a given value.

**Example 1: Using $eq to Match Field Value:**

Query: Select all documents from the `products` collection where the value of the `price` field equals 899.

```javascript
db.products.find({
    price: { $eq: 899 }
}, {
    name: 1,
    price: 1
})
```

**Example 2: Using $eq with Embedded Documents:**

Query: Select documents where the value of the `ram` field in the `spec` document equals 4.

```javascript
db.products.find({
    "spec.ram": { $eq: 4 }
}, {
    name: 1,
    "spec.ram": 1
})
```

**Example 3: Using $eq with Arrays:**

Query: Select documents where the `color` array contains an element with the value "black".

```javascript
db.products.find({
    color: { $eq: "black" }
}, {
    name: 1,
    color: 1
})
```

**Example 4: Using $eq with Dates:**

Query: Select documents with `releaseDate` equal to 2020-05-14.

```javascript
db.products.find({
    releaseDate: { $eq: new ISODate("2020-05-14") }
}, {
    name: 1,
    releaseDate: 1
})
```

**Introduction to the MongoDB $lt Operator:**

The `$lt` operator is a comparison query operator that allows you to select documents where the value of a field is less than a specified value.

**Example 1: Using $lt to Match Field Values:**

Query: Select documents where `price` is less than 799.

```javascript
db.products.find({
    price: { $lt: 799 }
}, {
    name: 1,
    price: 1
})
```

**Example 2: Using $lt with Embedded Documents:**

Query: Select documents where the value of the `screen` field in the `spec` document is less than 7.

```javascript
db.products.find({
    "spec.screen": { $lt: 7 }
}, {
    name: 1,
    "spec.screen": 1
})
```

**Example 3: Using $lt with Arrays:**

Query: Select documents where the `storage` array has at least one element less than 128.

```javascript
db.products.find({
    storage: { $lt: 128 }
}, {
    name: 1,
    storage: 1
})
```

**Example 4: Using $lt with Dates:**

Query: Select documents with `releaseDate` before 2015-01-01.

```javascript
db.products.find({
    releaseDate: { $lt: new ISODate('2015-01-01') }
}, {
    name: 1,
    releaseDate: 1
})
```

**Introduction to the MongoDB $lte Operator:**

The `$lte` operator is a comparison query operator that selects documents where the value of a field is less than or equal to a specified value. The syntax is the same as `$lt`.

**Introduction to the MongoDB $gt Operator:**

The `$gt` operator is a comparison query operator that selects documents where the value of a field is greater than a specified value. The syntax is the same as `$lt`.

**Introduction to the MongoDB $gte Operator:**

The `$gte` operator is a comparison query operator that selects documents where the value of a field is greater than or equal to a specified value. The syntax is the same as `$lt`.

**Introduction to the MongoDB $ne Operator:**

The `$ne` operator is a comparison query operator that selects documents where the value of a field is not equal to a specified value. It includes documents that don't contain the field.

**Example 1: Using $ne to Match Field Values:**

Query: Select documents where `price` is not equal to 899.

```javascript
db.products.find({
    price: { $ne: 899 }
}, {
    name: 1,
    price: 1
})
```

**Example 2: Using $ne with Embedded Documents:**

Query: Select documents where the value of the `screen` field in the `spec` document is not equal to 9.7.

```javascript
db.products.find({
    "spec.screen": { $ne: 9.7 }
}, {
    name: 1,
    "spec.screen": 1
})
```

**Example 3: Using $ne with Arrays:**

Query: Select documents where the `storage` array does not contain an element with the value 128.

```javascript
db.products.find({
    storage: { $ne: 128 }
}, {
    name: 1,
    storage: 1
})
```

**Example 4: Using $ne with Dates:**

Query: Select documents where `releaseDate` is not equal to 2015-01-14.

```javascript
db.products.find({
    releaseDate: { $ne: new ISODate('2015-01-14') }
}, {
    name: 1,
    releaseDate: 1
})
```

**Introduction to the MongoDB $in Operator:**

The `$in` operator is a comparison query operator that selects documents where the value of a field matches any value in an array.

**Example 1: Using $in to Match Field Values:**

Query: Select documents where `price` is either 599 or 799.

```javascript
db.products.find({
    price: { $in: [699, 799] }
}, {
    name: 1,
    price: 1
})
```

**Example 2: Using $in with Arrays:**

Query: Select documents where the `color` array contains "black" or "white".

```javascript
db.products.find({
    color: { $in: ["black", "white"] }
}, {
    name: 1,
    color: 1
})
```

**Example 3: Using $in with Regular Expressions:**

Query: Select documents where the `color` array contains elements matching /^g+/ or /^w+/ regular expressions.

```javascript
db.products.find({
    color: { $in: [/^g+/, /^w+/] }
}, {
    name: 1,
    color: 1
})
```

**Introduction to the MongoDB $nin Operator:**

The `$nin` operator is a comparison query operator that selects documents where the value of a field is not equal to any value in an array or where the field does not exist.

**Example 1: Using $nin to Exclude Values:**

Query: Select documents where `price` is neither 599 nor 799.

```javascript
db.products.find({
    price: { $nin: [699, 799] }
}, {
    name: 1,
    price: 1
})
```

**Example 2: Using $nin with Arrays:**

Query: Select documents where the `color` array does not contain "black" or "white".

```javascript
db.products.find({
    color: { $

nin: ["black", "white"] }
}, {
    name: 1,
    color: 1
})
```

**Example 3: Using $nin with Regular Expressions:**

Query: Select documents where the `color` array does not contain elements matching /^g+/ or /^w+/ regular expressions.

```javascript
db.products.find({
    color: { $nin: [/^g+/, /^w+/] }
}, {
    name: 1,
    color: 1
})
```

</details>

