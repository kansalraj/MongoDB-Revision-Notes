# MongoDB-Revision-Notes

Summary of Commonly Used MongoDB Data Types:

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

In this tutorial, you've learned about the most commonly used MongoDB data types, including null, boolean, number, string, date, regular expression, array, embedded document, and Object ID. These data types provide the foundation for structuring and storing diverse data within MongoDB documents.
