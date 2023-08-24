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



