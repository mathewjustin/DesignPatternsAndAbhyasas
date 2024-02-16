From Painful Tables to Performance Bliss: My Journey with Database Partitioning - Part II

Skewed workloads and Relieving Hot Spots



Imagine you have a library with books categorized by their first letter (A-Z). This is like partitioning data based on a key (like the first letter of a book title).

Problem: One letter (say, "X") becomes super popular (a celebrity author!). Everyone wants to read "X" books, causing a "hot spot" (overcrowding) in the "X" section.

Hashing doesn't fix it: Even if you assign different "buckets" based on a hash of the title, all "X" books still end up in the "X" bucket.

Solution 1: Split the key: Add a random number to each "X" book title (e.g., "X123", "X456"). This spreads them across different buckets, reducing the crowd in "X".

Drawback: Now you need to check all buckets with "X" to find all the books (more work for reading).

Solution 2 (future): Imagine the library magically adjusts shelves based on popularity, automatically spreading out the "X" books.

Takeaway: Choose the solution that best fits your needs. Splitting keys helps with hot spots but adds complexity. Future systems might handle this automatically.



Partitioning and Secondary Indexes




A secondary index usually doesn't identify a record uniquely but rather is a way of searching for occurences of a particular value; find all action by user 123, find all articles containing the word hogwash, find all cars whose color is red. In these statements you can see we use a secondary index for our query. 

This is essential for any database design. The issue with secondary indexes are they don't map neatly to partitions. This happens due to non uniqueness, for example find all action by user means find all actions| filter by user, so the find all will go search on all partition. This is a simple example for this problem.

There are two main approaches to partitioning a database with secondary indexes : document-based partitioning and term based partitioning. 



Partitioning Secondary Indexes by Document.


 

If you look at this image you can see within each partition there is another secondary index created.  So if you want to search for red cars, you need to send the query to all partitions, and combine all the results you get back.  In this approach you can notice each partition creates its own secondary index and when you are writing to it you only need to deal with the partition that contains the document ID that you are writing. For this exact reason a Document-Partitioned index is also known as local index.

Querying this kind of partitioned database is known as scatter/gather, and it can make read queries on secondary indexe quite expensive. Even if you query the partition in parallel scatter/gather  is prone to tail latency amplifications. Nevertheless it is a widely used approach. 

On the next blog we will learn more about partitioining from Martin Klepmann's "Designing Data intensive Applications



