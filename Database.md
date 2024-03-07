## PostgreSQL

### Q : What are the advantages of PostgreSQL?
A : Some of the advantages of PostgreSQL are open-source DBMS, community support, ACID compliance, diverse indexing techniques, full-text search, a variety of replication methods, and diversified extension functions, etc.

### Q : char and varchar difference in sql
A : VARCHAR is variable length, while CHAR is fixed length.

SQL varchar stores variable string length whereas SQL char stores fixed string length. This means SQL Server varchar holds only the characters we assign to it and char holds the maximum column space regardless of the string it holds.

### Q : What is the name of the process of splitting a large table into smaller pieces in PostgreSQL?
A : The name of the process of splitting a large table into smaller pieces in PostgreSQL is known as table partitioning.

### Q : What is the maximum size for a table in PostgreSQL?
A : PostgreSQL provides unlimited user database size, but it doesn't provide an unlimited size for tables. In PostgreSQL, the maximum size for a table is set to 32 TB.

### Q : Which commands are used to control transactions in PostgreSQL?
A : The following commands are used to control transactions in PostgreSQL:

BEGIN TRANSACTION
COMMIT
ROLLBACK

### Q : index POSTGRESQL
A : An Index is the structure or object by which we can retrieve specific rows or data faster. Indexes can be created using one or multiple columns or by using the partial data depending on your query requirement conditions.

Index will create a pointer to the actual rows in the specified table.

You can create an index by using the CREATE INDEX syntax.

* types 

1. B-tree : The most common and widely used index type is the B-tree index. This is the default index type for the CREATE INDEX command, unless you explicitly mention the type during index creation. 

If the indexed column is used to perform the comparison by using comparison operators such as <, <=, =, >=, and >, then the  Postgres optimizer uses the index created by the B-tree option for the specified column.

2. Hash index : The Hash index can be used only if the equality condition = is being used in the query.

3. GiST

4. SP-GiST

5. GIN

6. BRIN

## MongoDB

### Q : What type of NoSQL database MongoDB is?
A : MongoDB is a document-oriented database. It stores the data in the form of the BSON(Binary JSON) structure-oriented databases. 
* We store these documents in a collection. Data stored in NoSQL db is mostly unstructured.
* Schema free dynamically typed data.

### Q : What is a Collection in MongoDB?
A : A collection in MongoDB is a group of MongoDB documents. It is similar to a table in relational databases but does not enforce a schema.

### Q : Explain Namespace?
A : namespace is the series of the collection name and database name.

### Q : What is capped collection?
A : In MongoDB, a capped collection is a special type of collection that has a fixed-size and maintains insertion order. Capped collections are often used for scenarios where you want to store a limited amount of data in a circular buffer fashion, and once the collection reaches its size limit, older documents are automatically removed to make room for new ones. This behavior is useful in scenarios such as logging, event tracking, or any use case where you are interested in the most recent data and do not need historical data beyond a certain point.

### Q : How to optimize mongodb query
A : 
* Use Indexes:
Properly designed indexes can significantly improve query performance. Analyze your query patterns and create indexes on fields used in query conditions, sorting, and grouping.
Use the explain method to understand how MongoDB is executing a query and whether indexes are being utilized.

* Avoid Large Result Sets:
Limit the number of documents returned by a query using the limit() method. Fetching a large number of documents can negatively impact performance.
Use pagination techniques for displaying large result sets in smaller chunks.

* Projection:
Only retrieve the fields you need by using the projection parameter. This reduces the amount of data transferred over the network and can improve query performance.
Avoid using find() without projection if you only need a subset of fields.

* Avoid Unnecessary Queries:
Minimize the number of queries by fetching related data in a single query using $lookup (for aggregation) or embedding data where appropriate.
Consider denormalization in scenarios where it improves query performance.

* Use Aggregation Pipeline Wisely:
Optimize complex queries using the aggregation pipeline. Aggregation stages like $match, $project, $group, and $sort can be used to filter and transform data efficiently.
Be mindful of the order of stages in the aggregation pipeline to take advantage of indexes.

* Avoid Regular Expressions (Regex) if Possible:
Regular expressions can be resource-intensive. If you can achieve the same result with other query operators, it might be more efficient.

* Monitor and Analyze Query Performance:
Use tools like MongoDB's built-in profiler, MongoDB Compass, or third-party monitoring tools to monitor and analyze query performance.
Identify slow queries and understand their execution plans.

* Update MongoDB Version:
Ensure you are using a recent version of MongoDB, as each release often includes performance improvements and optimizations.

### Q : What is gridfs?
A : Mongo has limitation of storing max 16 MB file so if it is more than that then we can use gridfs.GridFS is a specification for storing and retrieving large files in MongoDB. It is a way to work with files that exceed the BSON document size limit of 16 MB, which is the maximum size MongoDB can store in a single document. GridFS breaks the files into smaller chunks and stores each chunk as a separate document, allowing MongoDB to handle large files efficiently.

* Chunks Collection:
The actual binary data of the file is stored in a separate collection, usually named fs.chunks. Each chunk is a document containing a portion of the file's binary data.

* Chunk Size:
GridFS divides large files into smaller chunks, and each chunk is typically 255 KB in size by default. You can configure the chunk size based on your requirements.

* File Metadata:
The fs.files collection stores metadata related to each file, such as filename, content type, size, and any user-defined metadata.

### Q : Explain Indexes in MongoDB?
A : 
* Indexing in MongoDB is the process of creating indexes (similar to database indexes in SQL) to improve query performance. Indexes allow MongoDB to locate data more quickly, reducing the amount of data that needs to be scanned.

* In MongoDB, we use Indexes for executing the queries efficiently; without using Indexes, MongoDB should carry out a collection scan, i.e., scan all the documents of a collection, for selecting the documents which match the query statement. If a suitable index is available for a query, MongoDB will use an index for restricting the number of documents it should examine.

* Single field Index
* Compound Index
* Multikey Index
* Geospatial Indexes
* Text Index
* Hash Index
* Wildcard Index

### Q : What is a replica set?
A : We can specify the replica as a set of the mongo instances which host a similar data set. In the replica set, one node will be primary, and another one will be secondary. We replicate all the data from the primary to the secondary nodes.

### Q : What are Primary and Secondary Replica sets?
A : Primary and master nodes are the nodes that can accept writes. MongoDB's replication is 'single-master:' only one node can accept write operations at a time.

* Secondary and slave nodes are read-only nodes that replicate from the primary.

* MongoDB achieves high availability through features like replica sets, which maintain multiple copies of data across different servers. If one server fails, another can take over to ensure continuous service.

* A replica set is a group of MongoDB servers that maintain the same data set. It provides high availability and fault tolerance by allowing one server to automatically take over if another fails.

### Q : Explain Sharding and Aggregation in MongoDB?
* Aggregation: Aggregations are the activities that handle the data records and give the record results.The Aggregation Framework is a powerful tool in MongoDB for processing and transforming documents in a collection. It supports various operations such as filtering, grouping, sorting, and projecting to analyze and aggregate data.

* Sharding: Sharding means storing the data on multiple machines.Sharding is a method used to distribute data across multiple machines. In MongoDB, it involves splitting a collection's data across different servers to enable horizontal scaling and accommodate large datasets.

### Q : What does ObjectId contain?
ObjectId contains the following:

* Client machine ID
* Client process ID
* Byte incremented counter
* Timestamp

## Diff between both DB

| SQL      | MongoDB |
| ----------- | ----------- |
| Represented in tables      | Represented in documents       |
| Predifined Schema   | Dynamic Schema        |
| Vertically Scalable   | Horizontally scalable        |
| Supports Join   | Does not support join        |


### Q : Explain Vertical Scaling and Horizontal Scaling?
A : 
* Vertical Scaling: Vertical Scaling increases storage and CPU resources for expanding the capacity. SQL databases are vertically scalable

* Horizontal Scaling: Horizontal Scaling splits the datasets and circulates the data over multiple shards or servers. NoSQL databases are horizontally scalable

### Q :When to use mongodb and postgresql
The choice between MongoDB and PostgreSQL depends on the specific requirements of your application, the nature of your data, and the use cases you need to address. Both databases have distinct features and strengths that make them suitable for different scenarios. Here are some considerations to help you decide when to use MongoDB or PostgreSQL:

**Use MongoDB When:**

1. **Flexible Schema:**
   - If your data structure is dynamic and can evolve over time, MongoDB's flexible schema (document-oriented) may be a good fit. It allows you to store documents with different fields in the same collection.

2. **Scalability:**
   - MongoDB excels at horizontal scaling, making it suitable for applications that need to handle large amounts of data and traffic. It supports sharding, allowing you to distribute data across multiple servers.

3. **JSON/BSON Document Storage:**
   - If your application works with JSON-like documents or BSON (Binary JSON), MongoDB's document storage model provides a natural way to represent and query data.

4. **Agile Development:**
   - MongoDB is well-suited for agile development environments where the data model might change frequently during development. Its dynamic schema accommodates changes without requiring a predefined schema.

5. **Complex Data Structures:**
   - If your application requires complex nested data structures or arrays, MongoDB's document model allows you to store and query such data efficiently.

6. **Geospatial Data:**
   - MongoDB has strong support for geospatial indexing and queries, making it a good choice for applications that work with location-based data.

7. **Real-time Analytics:**
   - For scenarios where real-time analytics and data processing are essential, MongoDB's ability to handle large volumes of data with low-latency reads can be advantageous.

**Use PostgreSQL When:**

1. **Structured Data with ACID Compliance:**
   - If your application requires a relational database with support for transactions and strict ACID compliance, PostgreSQL is a strong choice. It enforces a rigid schema, ensuring data consistency.

2. **SQL Query Language:**
   - If your team is already familiar with SQL or if your application relies heavily on complex SQL queries, PostgreSQL's rich set of SQL features and extensions can be beneficial.

3. **Multi-table Joins:**
   - If your data model involves many-to-many relationships and complex queries involving multiple tables, PostgreSQL's relational nature and robust support for joins make it suitable.

4. **Data Integrity and Constraints:**
   - When data integrity, referential integrity, and the enforcement of constraints are critical, PostgreSQL provides strong support for enforcing data integrity rules.

5. **Mature Ecosystem:**
   - PostgreSQL has been around for a long time, resulting in a mature ecosystem with a large number of extensions, tools, and community support.

6. **Advanced Data Types and Functions:**
   - If your application requires advanced data types, such as arrays, hstore, JSON, XML, or if you need to define custom functions and aggregates, PostgreSQL's extensibility can be advantageous.

7. **Complex Transactions:**
   - For applications that heavily rely on complex transactions, PostgreSQL's support for nested transactions and savepoints can be important.

In many cases, the choice between MongoDB and PostgreSQL may not be an either-or decision. Some applications benefit from using both databases in a polyglot persistence architecture, where each database is used for its strengths in specific areas. This approach allows developers to leverage the strengths of each database to meet the diverse requirements of an application.
