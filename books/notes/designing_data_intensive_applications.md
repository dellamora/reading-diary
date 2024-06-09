# Part 1: Foundations of Data Systems

### Chapter 1: Reliable, Scalable, and Maintainable Applications

The first chapter was focused on explaining some fundamental ways of thinking about data-intensive applications, what the book will cover, and an overview of what reliability, scalability, and maintainability are.

- **Realiability**: systems should prevent hardware faults, software faults and human error.

- **Scalability**: As the system expands, whether in terms of data volume, traffic volume, or complexity, it's essential to have viable strategies in place to manage and accommodate this growth effectively.

- **Maintainability**: systems should be easey to operate, simple and adaptable.

### Chapter 2: Data Models and Query Languages

Data models are important because they can determine how we think about the problem that we are solving. Applications are built ny layering one data model on top of another.

**SQL**: Based on the relational model proposed by [Edgar F. Codd](https://en.wikipedia.org/wiki/Edgar_F._Codd) the SQL is the best-known data modal today. Data is organized into `tables`, where each relation is an unordered collections of `rows`

**NoSQL**: Have gained popularity because they handle massive amounts of data and high-speed writing better than regular databases. They are also free and open source, making them ideal for unique searches regular databases can't handle, and they offer more freedom in data management.

**ORM: The Object-Relational Mismatch**: Is request just one query because the relavant data are more easy to get it than creating a lot of queries because there are a lot of tables relations and the book cover some examples

(I just got lazy and didn't write more notes about this chapter)

### Chaper 3: Storage and Retrieval

A database needs to do two things: **store data and retrieve data**.

- know how databse handles storage and retrieval internally is important to select a storage engine that is appropriate for the kind of data you have and the kind of access patterns your application requires.

**Data Structures**: The most common data structures used in databases are `hash indexes`, `search trees`, and `log-structured storage`.

**Hash Indexes**: A hash index consists of an array of `buckets`, each of which contains a few `keys` and `pointers` to the records that have that key. The hash function determines which bucket a key is assigned to.

- **Bitcask** is a storage engine that uses hash indexes and well suited to situations where the value for a key is being updated frequently.

**B-Trees and LMS-Trees**: B-Trees are a generalization of binary search trees in which each node can contain more than two children. B-Trees are well suited to storing data on disk, because they are optimized for reading and writing large blocks of data. LMS-trees are a variation of B-Trees that are optimized for SSDs.

- **Downsides of LSM-Trees**

  - The process of merging segments is called compaction, and it can interfere with the performance of ongoing reads and writes. - Overhead: LSM-trees have more overhead than B-Trees because they have to maintain more data structures.

  - In high-write-throughput scenarios, LSM-Tree databases struggle to balance disk bandwidth between initial writes and ongoing compaction. Initially, when the database is empty, all disk bandwidth is used for writes. However, as the database grows, more bandwidth is needed for compaction. Without careful configuration, this can lead to a backlog of unmerged segments, decreased read performance, and potential disk space exhaustion. Effective management and monitoring of compaction are crucial to avoid these issues.

**Log-Structured Storage**: Log-structured storage engines write new data to the end of a sequentially written log, and periodically merge segments of the log into a new segment.

**Other Indexing Structures**: The book also covers secondary indexes, multi-column indexes ,full-text search / fuzzy indexes.

- secondary indexes: A secondary index is an index that is based on a field that is not the primary key. Secondary indexes are used to speed up queries that search for records based on a field that is not the primary key.

- Multi-column indexes: A multi-column index is an index that is based on more than one field. Multi-dimiensional are a general way of querying several columns at once.

```SQL
SELECT * FROM restaurants WHERE latitude > 51.4946 AND latitude < 51.5079
 AND longitude > -0.1162 AND longitude < -0.1004;
```

- Full-text search / fuzzy indexes: Full-text search is a technique for searching a document or a collection of documents for a word or a phrase. Fuzzy indexes are used to search for records that are similar to a given record. (Elasticsearch is a popular search engine that uses fuzzy indexes)

**Keeping everything in memory**: The book also covers the use of in-memory databases.

**OLAP VS OLTP**: The difference between OLTP
and OLAP is not always clear-cut, but some typical characteristics are listed below.
| Property | Transaction Processing Systems (OLTP) | Analytic Systems (OLAP) |
|-------------------------------|-----------------------------------------------|-------------------------------------------------|
| Main Read Pattern | Small number of records per query, fetched by key | Aggregate over large number of records |
| Main Write Pattern | Random-access, low-latency writes from user input | Bulk import (ETL) or event stream |
| Primarily Used By | End user/customer, via web application | Internal analyst, for decision support |
| Data Representation | Latest state of data (current point in time) | History of events that happened over time |
| Dataset Size | Gigabytes to terabytes | Terabytes to petabytes |

```text
"On a high level, we saw that storage engines fall into two broad categories: those opti‐
mized for transaction processing (OLTP), and those optimized for analytics (OLAP)."
```

**Data Warehousing**: Data warehousing is the process of collecting, storing, and managing data from various sources to provide meaningful business insights. It is a blend of technologies and components which allows the strategic use of data.

### Chapter 4: Encoding and Evolution

**Evolvability**: The ability to make changes to a system in the future, such as adding new features or fixing bugs.

- For server-side applications, you can perform rolling upgrades, deploying the new version gradually to a few nodes at a time, ensuring smooth operation before moving to others. This minimizes downtime, enabling more frequent releases.

- Client-side applications rely on users to install updates, which may cause delays in adoption.

- Backward compatibility is the ability of a system to accept input intended for a later version of itself.

- Forward compatibility is the ability of a system to accept input intended for a later version of itself.

**Formats for Encoding Data**: Programs usually work with data in diferents representations, so we need some kind of translations between them. The book covers some of the most common formats for encoding data.

**Language-Specific Formats**: Some languages have built-in support for encoding objects into byte sequences. While convenient for in-memory operations, these libraries lack cross-language compatibility. Decoding may require instantiating arbitrary classes, posing security risks. Versioning and efficiency are also challenges, as handling different object versions can be complex.

(There are a lot of examples in the book, but I didn't write them down)

**JSON, XML, and Binary Variants**: JSON and XML are popular for encoding data for interchange between systems. They are human-readable, but verbose and slow to parse. Binary variants are more efficient, but lack human readability

**Avro**: Avro is a binary encoding format that is smaller and faster to encode and decode than JSON. It is also a schema-based format, meaning that the schema is included in the encoded data, allowing for forward and backward compatibility.

(Note there a lot of nice things to say about Avro, but I haven't written them down.
)

- Define Schema: Avro schemas are defined using JSON. The schema defines the fields and types of the data being encoded.
- Schema Evolution: Avro supports schema evolution, meaning that the schema can change over time. New fields can be added, fields can be removed, and fields can be renamed. Avro also supports default values for fields, allowing for backward compatibility.
- Writer Schema and Reader Schema: Avro supports the concept of a writer schema and a reader schema. The writer schema is the schema used to encode the data, and the reader schema is the schema used to decode the data. The reader schema can be different from the writer schema, allowing for forward and backward compatibility.

**Dataflow Throught Databases**: Basically, in a database, the process that writes to the database encodes the data and the process that reads from the databse decodes it.

- Different values written at different times may be encoded differently, so the database must be able to handle multiple encodings of the same field. This is called **schema evolution**.

**Dataflow Throught Services**: When you have proceses that need to communicate over a **network**, there are a few differents ways of arranging that communication.

**REST and HTTP**: REST is an architectural style for building distributed systems. It is based on the principles of the web, such as URLs, HTTP methods, and hypermedia. RESTful systems are stateless, meaning that each request from the client to the server must contain all the information necessary to understand the request. RESTful systems are also cacheable, meaning that responses can be cached to improve performance.

**Remote Procedure Calls (RPC)**: RPC is a synchronous request-response protocol. The client sends a request to the server and waits for a response. The server processes the request and sends a response back to the client. The client is blocked until the server responds.

**Message brokers (also called a message queue or message-oriented middleware)**: facilitates communication between different applications by receiving messages from one application and delivering them to another. It acts as an intermediary, enabling decoupled communication and allowing applications to interact without direct awareness of each other.

```text
"in general, message brokers are used as follows: one process sends a message to a named queue or topic, and the broker ensures that the message is delivered to one or more consumers of or subscribers to that queue or topic. There can be many producers and many consumers on the same topic."

```

**Distributed actor frameworks**: A distributed actor framework is a framework for building distributed systems using the actor model. The actor model is a model of concurrent computation that treats actors as the universal primitives of concurrent computation. In response to a message that it receives, an actor can make local decisions, create more actors, send more messages, and determine how to respond to the next message received.

**SUMMARY**

- In databases, data is encoded by the writing process and decoded by the reading process.
- RPC and REST APIs involve encoding a request by the client, decoding it by the server, then encoding a response by the server and decoding it by the client.
- In asynchronous message passing, such as with message brokers or actors, nodes exchange encoded messages, with senders encoding and recipients decoding them for communication.
