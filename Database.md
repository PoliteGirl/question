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

* The Aggregation Framework is a powerful tool in MongoDB for processing and transforming documents in a collection. It supports various operations such as filtering, grouping, sorting, and projecting to analyze and aggregate data.

### Q : Explain Sharding and Aggregation in MongoDB?
* Aggregation: Aggregations are the activities that handle the data records and give the record results.The Aggregation Framework is a powerful tool in MongoDB for processing and transforming documents in a collection. It supports various operations such as filtering, grouping, sorting, and projecting to analyze and aggregate data.

* Sharding: Sharding means storing the data on multiple machines.Sharding is a method used to distribute data across multiple machines. In MongoDB, it involves splitting a collection's data across different servers to enable horizontal scaling and accommodate large datasets.

### Q : What does ObjectId contain?
ObjectId contains the following:

* Client machine ID
* Client process ID
* Byte incremented counter
* Timestamp

### Q : Explain Vertical Scaling and Horizontal Scaling?
A : 
* Vertical Scaling: Vertical Scaling increases storage and CPU resources for expanding the capacity. SQL databases are vertically scalable

* Horizontal Scaling: Horizontal Scaling splits the datasets and circulates the data over multiple shards or servers. NoSQL databases are horizontally scalable

## Diff between both DB

| SQL      | MongoDB |
| ----------- | ----------- |
| Represented in tables      | Represented in documents       |
| Predifined Schema   | Dynamic Schema        |
| Vertically Scalable   | Horizontally scalable        |
| Supports Join   | Does not support join        |


