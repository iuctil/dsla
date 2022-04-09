---
title: "Quick Comparions of NoSQL Databases"
description: "Quick Comparions of NoSQL Databases"
lead: "Quick Comparions of NoSQL Databases"
keywords: 
    - Data Science
    - NoSql
contributors:
    - Leon Hwang 
date: 2022-03-01T00:00:00+00:00
lastmod: 2022-03-19T00:00:00+00:00
draft: false
toc: true
plotly: false
images: []
weight: 100
menu:
    docs:
        parent: "KnowledgeObjects"
---
# Quick Comparions of NoSQL Databases

Over the past decade, the interest and demand of NoSQL databases have increased dramatically. 

Relational databases are known for robustness and consistency, and have been the major players in the DB market for a long time. However, when they handle large-scale data, they suffer from scalability and bad performance.  NoSQL is complementary to SQL and it has various formats for storage that can support large volume of different types of data with high velocity.

There are hundreds of different NoSQL databases available today and it is difficult to find the right database for your task.  We will compare several popular NoSQL databases.

![NoSQL Database Types](/images/NoSQL-DB-Types.png "NoSQL Database Type")


NoSQL DBs are not an exception to CAP Theorem which states that a distribute data store is unable to provide all three of consistency, availability, and partition-tolerance at the same time.

![CAP Theorem](/images/NoSQL-DB-Types.png "CAP Theorem")



## Characteristics of NoSQL Databases

- NoSQL databases, in general, can be categorized into key-value, document, and column stores, or graphs based on their storage model, and each offers different solutions.

- Key-value store DBs are simplest and designed to store data with no schema Column Store DBs are designed to store large volumes of columns.

- Document base DBs are more complex data and designed to store, manage and extract info in and from document.

- Graph DBs are based on on graphs that have interconnected components and relations between them.

  

| Parameter    | Column-Oriented      | Graph-Based          | Key-Value                | Document-Oriented               |
| ------------ | -------------------- | -------------------- | ------------------------ | ------------------------------- |
| Storage      | Columns              | Nodes and edges      | Unique Key with value    | XML, JSON, BSON                 |
| Applications | Sparse data          | Social connections   | Indexing                 | Programming objects storage     |
| Examples     | Big Table, Cassandra | Neo4j, InfoGrid      | Dynamo, Oracle NoSQL     | MongoDB, CouchDB                |
| Format       | Flexible Schema      | Dynamic Schema       | Schema-less              | Schema-less                     |
| Advantages   | Scalability          | High fault tolerance | Less query response time | Generalized storage for objects |
| Flexibility  | Average              | High                 | High                     | High                            |
| Performance  | Good                 | Varying              | Good                     | Good                            |
| Scalability  | High                 | Varying              | High                     | Varying                         |
| Complexity   | Low                  | High                 | Low                      | Low                             |



|                         | Aerospike                                                    | Cassandra                       | Couchbase                                                    | CouchDB                                                      | Hbase                                          | MongoDB                                        | Voldemort                              |
| ----------------------- | ------------------------------------------------------------ | ------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------------------------------- | ---------------------------------------------- | -------------------------------------- |
| **Category**            | Key-Value                                                    | Column-Store                    | Document-Store                                               | Document-Store                                               | Column-Store                                   | Document-Store                                 | Key-Value                              |
| **CAP**                 | AP                                                           | AP/CP                           | CP                                                           | AP                                                           | CP                                             | CP                                             | AP                                     |
| **Consistency**         | Configurable  (several options)                              | Configurable  (several options) | Eventual Consistency                                         | Eventual Consistency                                         | Configurable (strong and eventual consistency) | Configurable  (several options)                | Read-Repair (client handles conflicts) |
| **Durability**          | Notified written to desired nodes                            | Configurable  (several options) | Configurable  (several options)                              | Configurable  (notified written to at least one disk)        | Configurable  (several options)                | Configurable  (several options)                | Notified written to desired nodes      |
| **Querying**            | Internal API                                                 | Internal API, SQL like (CQL)    | Internal API (MapReduce)                                     | Internal API (MapReduce)                                     | Internal API                                   | Internal API, MapReduce, complex query support | Internal API (get, put, delete)        |
| **Concurrency Control** | Read-committed isolation level (support for optimistic concurrency control) | MVCC                            | MVCC (application can select Optimistic or Pessimistic locking) | MVCC (application can select Optimistic or Pessimistic locking) | Optimistic locking with MVCC                   | Master-slave with multi-granularity locking    | Optimistic locking with MVCC           |
| **Partitioning Scheme** | Proprietary (Paxos based)                                    | Consistency Hashing             | Consistency Hashing                                          | Consistency Hashing (third party)                            | Ranged Based                                   | Consistency Hashing                            | Consistency Hashing                    |
| **Native Partitioning** | Yes                                                          | Yes                             | Yes                                                          | No                                                           | Yes                                            | Yes                                            | Yes                                    |



## Software Quality Attributes

| Quality Attribute   | Description                                     |
| ------------------- | ----------------------------------------------- |
| **Availability**    | Percent of Up-time                              |
| **Consistency**     | Transaction guarantee                           |
| **Durability**      | Validity of data in disk                        |
| **Maintainability** | Easiness to operate, upgrade, repair, and debug |
| **Performance**     | Optimization for read and write                 |
| **Recovery Time**   | Time to recover and stabilize from a failure    |
| **Reliability**     | Probability of no failure                       |
| **Robustness**      | Ability to handle errors                        |
| **Scalability**     | Ability to handle growing workloads             |

The research finds that each system has its strength and weakness and there is no one-size-fits-all solution. This table shows the evaluation of the popular NoSQL databases and their strengths and weaknesses. 

|                        | Aerospike | Cassandra | Couchbase | CouchDB | HBase | MongoDB | Voldemort |
| ---------------------- | --------- | --------- | --------- | ------- | ----- | ------- | --------- |
| **Availability**       | `++`      | `++`      | `++`      | `++`    | `-`   | `-`     | `++`      |
| **Consistency**        | `++`      | `++`      | `+`       | `+`     | `=`   | `++`    | `+`       |
| **Durability**         | `-`       | `+`       | `+`       | `-`     | `+`   | `+`     | `+`       |
| **Maintainability**    | `+`       | `=`       | `+`       | `+`     | `-`   | `=`     | `-`       |
| **Read-Performance**   | `+`       | `-`       | `++`      | `=`     | `-`   | `++`    | `+`       |
| **Write-Performance**  | `+`       | `++`      | `+`       | `-`     | `+`   | `-`     | `++`      |
| **Recovery Time**      | `++`      | `--`      | `+`       | `?`     | `?`   | `++`    | `?`       |
| **Reliability**        | `-`       | `+`       | `-`       | `+`     | `+`   | `++`    | `?`       |
| **Robustness**         | `+`       | `+`       | `=`       | `=`     | `--`  | `=`     | `?`       |
| **Scalability**        | `++`      | `++`      | `++`      | `-`     | `++`  | `-`     | `+`       |
| **Stabilization Time** | `--`      | `+`       | `+`       | `?`     | `?`   | `--`    | `?`       |

(`++`: Great, `+`: Good, `=`: Average, `-`: Mediocre, `--`: Bad, `?`: Unknown/N.A.)



## References
1. Bathla, G., Rani, R., & Aggarwal, H. (2018). Comparative study of NoSQL databases for big data storage. *International Journal of Engineering & Technology*, *7*(2.6), 83. https://doi.org/10.14419/ijet.v7i2.6.10072
2. Lourenço, J. R., Cabral, B., Carreiro, P., Vieira, M., & Bernardino, J. (2015). Choosing the right NoSQL database for the job: a quality attribute evaluation. *Journal of Big Data*, *2*(1). https://doi.org/10.1186/s40537-015-0025-0
