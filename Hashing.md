## Hashing
<hr>

Hashing is an action you can perform to transform an arbitary piece of data into 
a fixed size value. In terms of sysdesigning it can be an ip address, usernamme ..etc.


### Imagine we have a set of clients -->Hits a single LB --> Multiple Servers.

<p>
Now the LB has to have some kind of sever selection strategy to select the server. We discussed Random selection, Sequantial selection..etc.
A lot of them are fine in face value but it can introduce some problems.
Imagine a request which is very expensive, one way to handle this is to implement caching. Evey request that goes through say server A. Server A will check 
if the response is cached, if so it will return the cached response. 
</p>

<p>

</p>
