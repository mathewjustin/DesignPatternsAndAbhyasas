**Caching**
We use a lot of caching in our algorithms. The reason why we do caching is to memorize something 
which is precomputed and speadup the program. In system design caching is basically done to improve
the latency of a system. 

Caching is a gonna be a way of storing data in a location which is faster than the true source.
You can have caching at the client level so that it no loger has to go to server to retrieve.
May be you can cache at server, a server can avoid going to DB. You can even have cahcing at DB level,
You can even have caching at hardware level. 

For example: CPU caches, these will live at the CPU level, which helps to retrieve data faster from memory w.r.t CPU.

Lets see some concrete examples,

1. You are doing a lot of network requests and you need to avoid these. 
    Client <-- >Server <--> DB
    Client < [Cache] >Server <--> DB
2. Another is if you are doing a very computationaly long operation.
    
  --> Server (An algo which has poor time complexity) [Cache]

3. Imagine we have multiple servers instead of just one server. Here you can have cahing not to increase 
   performance, but to avoid overloading DBs. Here we will end up having less DB read-calls.

Some concrete example for cahcing in action: 
   
  If you go on leetcode, and in the list of questions. There will be a loading icon.
  If you go to another pare without closing tab, and go back to the previous questions list.
  Then the list of questions list will appear immediately. This is an example for caching a static content. 
  
Another concrete example :
  Running code on leetcode, it can take an average 1 sec. When people run code,
  with leetcodes, own solution they don't need to do the computation they can store the results and return it.
  This caching will be at server level. May be on Redis.

How to implement this ? Hash it down and store it as key and value as the results. 
In this way we can avoid that additional 1 sec of running the code.

<hr>

User write a POST --> Server will store it in a DB.

Now if you want to cache this FB Post. Now we have 2 sources of truth. 
Now if we edit a POST. 

Behind the screen what happens is. Server will store it in the DB -->Then Refresh the cache.

We have two popular Caches in this case.

Write through cache.

In this case the data will be writeen in Cache and DB at the same time. 
The FB post is stored on DB and Server. When you edit the POST. Server override the cache,
then it writes to DB. 

The downside of this is you end up going to the DB. 

Second popular cache is Write Back Cache:

Edit the POST --> Server will only update the cache. 

Now your DB is outof date with Cache. Now your system will sync the data 
from server to DB on some scheduled time, or some asynchrosnus process.

Downside of this : If something happens to your server then you will lose your data. 
But ofcourse there is solutions to handle that. 

<hr>
Youtube commenting system.

Imaging you have multiple clients which contacts multiple servers to add comments. 
And one client who added a comment being edited by him. Imagine client 2 is seeing 
the unedited comment and replying to the stale comment. This would be very bad.

In this particular system the solution is to move the cache out of server and have a single cachine server like Redis.
So all clients will hit the same cahce. Now we no longer has to worry.

Youtube ViewCount
<hr>
It can be stale, because its not really end of the world. 
So in a system design interview we must ask questions like this to interviewer. 
May be we can use caching in naive way for data which doesn't have much relevence.

PitFalls of Cahing
<hr>
Caching static data is so easy.(Immutable data)
You should consider caching if data is immutable.
If you dont care about consistency then we can consider caching. 
If you are able to design system and you can properly evict data in a distributed system.
then you can consider caching.

**Eviction policies**

1. LRU policy: Least recently used policy. You can get rid of data which is least recently used
2. LFU policy: Least frequently used policy. You can get rid of least frequently used. LIFO or FIFO manner..

It is a very fundamental technique in sytem design.
