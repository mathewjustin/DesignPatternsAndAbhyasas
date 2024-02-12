From Painful Tables to Performance Bliss: My Journey with Database Partitioning - Part I
Ah, the early days of wrangling massive data tables! I vividly remember the struggle – slow queries, performance bottlenecks, and the ever-growing cloud bill. It was an uphill battle until we unearthed the magic bullet: database partitioning. Talk about a revelation! This newfound approach not only eradicated performance issues but also slashed computational costs.


But the story doesn't end there. My exploration revealed a treasure trove of partitioning techniques, each unlocking unique advantages. Inspired by "Designing Data-Intensive Applications", I embarked on a quest to master this data management superpower. This blog chronicles my learnings, shedding light on the various ways you can partition your data for optimal performance and cost-efficiency.



Every partition is a small database of its own. Each piece of data will belong to one partition. The main reason for having this small databases or we call partition is for scalability. Different partition can be placed in different nodes in a shared-nothing cluster(A cluster of nodes where nodes will be independent). 

Assume there is a query to fetch a row, the query will be performed by a node on its on partition. So to increase throughput just add more nodes. 



Partitioning and Replication 
Building on the previous statement, if every node has a partition, it implies that each node holds copies of all partitions. This ensures that even though each record belongs to a specific partition, it might still be present on multiple nodes for the sake of fault tolerance. 
                            



Partitioning by Key Range

Real-World Example: Imagine millions of IoT devices, each with a unique IMEI number and timestamps for sensor readings. We can leverage key-range partitioning by using the date as the key. However, a potential drawback arises: all data within a single day would reside in the same partition, leaving others idle.
Dual Partitioning: To address this and distribute the write load more evenly, we can introduce dual partitioning. We'll use both the date and the IMEI number as keys. This ensures data gets distributed across multiple partitions based on both date and device, preventing overloading of single partitions.

Querying: When fetching data from multiple sensors within a specific time range, separate range queries will be needed for each IMEI number. However, the overall performance gain often outweighs this drawback due to the efficient retrieval within each partition.

Personal Experience: This concept played a pivotal role in my career, saving the company millions. By implementing dual partitioning for range-based queries on massive IoT sensor data, we significantly improved performance and optimized resource utilization. This experience solidified the importance of understanding core concepts before designing any system.


Partitioning by Hash of Key
This is another very interesting partitioning concept. In contrast to key-range partitioning, we use a hash function to determine the partition of a given key. A good hash function takes skewed data and makes it uniformly distributed. Imagine you have a 32-bit hash function that takes a string. When you provide a new string, it returns a seemingly random number between 0 and (2 to the power of 32) - 1. Even if the input strings are very similar, their hashes are evenly distributed across that range of numbers.

Cassandra and Mongo uses MD5

Voldermort uses the Fowoler-Noll-Vo function.

Built-in hash functions of programming languages may not be suitable for data partitioning. For example, Java's hashCode() method can generate different hash values for the same key in different processes. In such cases, it's recommended to use separate hash implementations specifically designed for consistent key distribution across partitions. The figure below shows how partitioning by a well-chosen hash function actually works.




This is indeed a great technique for evenly distributing keys across partitions. The partition boundaries can be equally spaced or chosen pseudorandomly.
