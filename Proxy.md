**Proxies**
<hr>
<p>
In movies we seen this : We can't see the hackers because they are hiding behind the proxies
</p>


<p>
We will be covering 2 types of proxies. Reverse proxies and forward proxies.

Forward Proxy : It is a server it sits in between a client or a set of clients and
a server or a set of servers. Forward proxy is on the client side. If a client wants 
to communicate with a server, assuming fp is being configured, when client initiates the connection
with server. Then request will go to the forward proxy. Forward proxy will then forward the request to the server.
Then server gets the request but the server thinks that the request is coming from the forward proxy.
Client will always ask the forward proxy to get the data. Forward proxy will get the data from the server and 
then forward it to the client.

It basically hides the identity of the client. It is used for security reasons.
The source ip address of the client is hidden from the server. This is how VPN works in a simplified way.

This means a client will be able to access the server which is not accessible to the client.
</p>
<p>
Reverse Proxy : It is little trickier. Reverse proxies act on behalf of a server.
if a client wants to interact with a server. If the server is configured a reverse proxy. When client requests
data then the request will go to reverse proxy, and then reverse proxy will forward the request to the server. Server will return response 
to reverse proxy and reverse proxy will return the response to the client.

To the client there is only 1 entity. Client doesn't know that there is a reverse proxy in between.

Reverse proxies are realy useful. You might configure reverse proxy to filter out requests that you dont want.

If you want to cache something you can configure reverse proxy to cache the data. 
You can use reverse proxy as a load balancer. A load balancer is a server which distributes the load to multiple servers.
For instace you are designing a complex servers you might have bunch of servers and you can have a reverse proxy to serve as a load balancer.

</p>

<p>
Imagine you have a malicius client who wants to attack the server. If you have a reverse proxy in between then the reverse proxy will be the one who will be attacked. 
So the server will be safe. (Like i configured azure api management)
</p>

<p>
We can use NGINX as a reverse proxy. NGINX is a web server. It is a very popular web server. It is used by many companies.
it is pronouncer as engine x. It is a very powerful web server. It is very fast. It is very easy to configure. It is very easy to use.

in the nginx.conf file we can configure the reverse proxy.
</p>
