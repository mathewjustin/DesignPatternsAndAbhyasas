# Load Balancers.
<p>
The more requests are sends to the server. The more likely our servers are to become overloaded.
To handle this scenerio : We scale our application horizontally by adding more servers.

Vertical Scaling : Adding more resources to the existing server.
Horizontal Scaling : Adding more servers to the existing system.

Load Balancer : Distributes the incoming traffic across multiple servers.

Load balancer is a server itself and it basically has the job of distributing the incoming traffic to multiple servers.
It also has the ability to do health checks on the servers and make sure that the servers are healthy before sending the traffic to them.
With this we can achieve our goal of horizontal scaling.

### It will help our system will increase thruoghput.
### Also the servers ends up getting better latency because they are not overloaded with requests.
### It is actually a reverse proxy.
</p>

<p>

### DNS Round Robin : which is basically a type of load balancing happens at the DNS domain level.
### when a DNS query is made to get IP of the domain name, the multiple ip addresses are being returnes in a round robin fashion to the client.
### This is kind of load balanced

</p>

<p>
## Hardware Load Balancer: Scaling is harder.
## Software Load Balancer: Customizations and scaling is easier.

We will look into software loadbalancers.

How a LB knows it has to send the traffic to a particular server. When you add or remove a server from the pool, how does the LB know about it.
Sever info will get registered or deregistered from the LB.

LB can have pure random redirection, this is not a good idea. It could be possible that one server is getting all the traffic and other servers are not getting any traffic.
</p>
<p>
LB can be round robin. In this case we can make sure we are evenly distributing the traffic across all the servers.
</p>
<p>
Weighted Loadbalancing: We can assign weights to the servers. So that we can make sure that some servers are getting more traffic than others.
You might want to do that if one of your server is powerful than the other server. In this case we can have a ## Weigted Round Robin strategy.
</p>

<p>
Load based load balancing: We can have a load based load balancing strategy. In this case we can have a load balancer that is monitoring the load on the servers.
LB will check for health of the servers and if the server is healthy then it will send the traffic to the server.
This is a pretty good way of doing load balancing.
</p>

<p>
IP Based sever selection strategy: The ip address of the client will get hashed. 
Imagine we have 3 servers and we have 3 clients. We will hash the ip address of the client and we will get a number. If this number is 1 then we will send the traffic to server 1.
This is useful when we want to make sure that the same client is always going to the same server.
It will be helpful when we do server level caching. If we want to cache the data on the server side then we can use this strategy.
IP Based selection will maximize the cache hits.
</p>

<p>
Path based server seletion strategy : We can have a path based server selection strategy. In this case we can have a load balancer that is monitoring the path of the request.
All request related to running code on leetcode will be redirected to server 1. All request related to running code on hackerrank will be redirected to server 2.
All request related to payment will be redirected to server 3.

Imagine if we want to make big change on the server which running the code on leetcode. We can take that server out of the pool and we can do the changes.
All the other use cases will still work.
</p>

<p>

## It make sense to have multiple load balancers with multiple strategies. 

We can have multiple lbs in different part of the system. 
We can also have multiple lbs at the lb level itself. This is to avoid single point of failure.

</p>

<p>
nginx config for weighted round robin load balancing.

```
events { }
http{
    upstream myapp1 {
        server localhost:3000 weight=3;
        server localhost:3001;
      }
      
      server {
        listen 80;
        location / {
          proxy_set_header test-123 true
          proxy_pass http://myapp1;
        }
      }
}
```

In this case the LB will redirect the request to server 1 3 times and then it will redirect the request to server 2.
With this config on nginx level create 2 servers on port 3000 and 3001.
Once you start curling localhost:8081/hello  you will see that first 3 requests 
will be redirected to server 1 and then 1 request to server 2 and then again 3 requests to server 1 and then 1 request to server 2,.. and so on.
</p>
