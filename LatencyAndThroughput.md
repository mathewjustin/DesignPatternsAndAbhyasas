Lot of people knows the terms. 
But many doesn't quite understand what it really means.

Latency and Throughput are 2 important meassures. 

Latency : Basically how long it takes for data to get from one point in a system to another point
in a system. We might be talking about a network request. How long it takes a network call from 
client -> Server ->client (Latency).

If you are on a machine and reading something from disk. The time to read the data from disk
is also known as latency. Different things in system is going to have different latencies. Some 
is going to more latency and some will have less latency.

Roughly speaking, if you are reading 1 MB sequentialy from mem it can take 250ms. This is a very fast operation

1MB from memory -> 250 ms
1MB sequentially from SSD -> 1000ms

What is important to realize is that reading from mem is lot faster than SSD.

For instance you send

1 MB over a 1GB / sec network this is going to take 10000ms.

Here we are assuming we are sending this data between two system which is very close, ie we are not
even considering distance. So we need to consider this is a lot longer from reading something
from memory. 

1MB from HDD 20000 MS. This is going to be longer than sending something over the network.

If you are sending a PACKET. (1000-1500 bytes),
over the network CA to Netherlands and back to CA. This is going to take almost 150 000 MS. 
So sending a packet on roundtrip from CA to NETHARLANDS will take a lot more than reading
from SSD or HDD. The reason is basically here the electricity has to travel, it is slower
when it has to travel half way across the globe. 

Some systems might really care about having low latencies. Eg: Online Video Games.
When we talk about LAG in the video game it really means it has a high latency, it may mean
the server may located in a geographically long distance. If you play a video game this 150 000
will add up and will crate a bad user experience.

But when it comes to say websites its all about uptime they may not care about latencies.

##Throughput 

 Is how much work a machine can perform in a given point of time. When we talk about througput 
hwo much data can be transffered from one point in a system to another point in a system in a given 
amount of time. 

We meassure in MB/Sec, 1GB / Sec.

Imagine we have many clients and they request to one ##Server.
The throughput is how many requests this server can handle at a time. 
if we convert all the requests to bit then its all about how many bits this server can 
handle in a second. How do i optimize a sytem for throughput --> You pay for it. You pay to increase
throughput. It basically in most of the cases decided by cloud provider(It is a naive way to think about it anyway).

Imagine we have a system where we have a single server which handles many requests, 
a better way to fix this is to have multiple servers to have them handled(Multiple instances.)

Even though they are very much related they are not really correlated. You might have a system or a smaller part of the sytem which suportes
fast data transfer, then you may have component which will have slow data transfer. Then low latency
operations are kind of cancelled out. You cannot make assumptions about latency and throughput 
based on the others they are not correlated. 

##Now we can use these terms with more confidence.

