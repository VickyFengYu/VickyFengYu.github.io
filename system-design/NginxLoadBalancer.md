NGINX-Load Balancer
===================

https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/

https://www.nginx.com/resources/glossary/load-balancing/


**Load balancing** refers to efficiently distributing incoming network traffic across a group of backend servers, also known as a _server farm_ or _server pool_.

----------

Load Balancing Apache Tomcat Servers with Nginx
-------------

https://docs.nginx.com/nginx/deployment-guides/apache-tomcat-load-balancing-nginx-plus/
https://www.thegeekstuff.com/2017/01/nginx-loadbalancer/

if your enterprise application is running on Apache (or Tomcat), you can setup an 2nd instance of your enterprise application on Apache (or Tomcat) on a different server.

And then, you can put Nginx at the front-end, which will load balance between the two Apache (or Tomcat, or JBoss) servers.

![enter image description here](http://wx1.sinaimg.cn/small/66865de2gy1ft0dq0ltgzj20ej09rglj.jpg)

Configuration Instructions can been found in [ Load Balancing Apache Tomcat Servers with NGINX Open Source and NGINX Plus](https://docs.nginx.com/nginx/deployment-guides/apache-tomcat-load-balancing-nginx-plus/)


#### <i class="icon-folder-open"></i>


NGINX Load Balancing Deployment Scenarios
-------------

https://www.nginx.com/blog/nginx-load-balance-deployment-models/?_ga=2.3375664.16638012.1530869696-954523176.1530869696

#### <i class="icon-folder-open"></i>1: NGINX Plus Does All Load Balancing
![enter image description here](https://cdn-1.wp.nginx.com/wp-content/uploads/2014/08/nginx.png)

#### <i class="icon-folder-open"></i> 2: Parallel with a Legacy Hardware‑Based Load Balancer


![enter image description here](https://cdn-1.wp.nginx.com/wp-content/uploads/2014/08/nginxside3.png)


#### <i class="icon-folder-open"></i>3: Behind a Legacy Hardware‑Based Load Balancer

![enter image description here](https://cdn-1.wp.nginx.com/wp-content/uploads/2014/08/nginxbehind.png)

----------

Proxying HTTP Traffic to a Group of Servers
-------------

https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/

To use NGINX Plus or NGINX to load balance HTTP traffic to a cluser of servers, first you should  define the group with the  upstream directive. The directive is placed in the http context.

#### <i class="icon-pencil"></i> 

#### <i class="icon-pencil"></i>


----------

Load Balancing Algorithms
-------------

https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/


#### <i class="icon-pencil"></i>Round Robin

Round Robin – Requests square measure distributed equally across the servers, with server weights taken into thought. This technique is employed by default (there is not any directive for enabling it):

    upstream backend {
	   server backend1.example.com;
	   server backend2.example.com;
	}


#### <i class="icon-pencil"></i>Least Connections

Least Connections – a call for participation is distributed to the server with the smallest amount range of active connections, once more with server weights taken into consideration:

    upstream backend {
	    least_conn;
	    server backend1.example.com;
	    server backend2.example.com;
	}

#### <i class="icon-pencil"></i>IP Hash

IP Hash – The server to that a call for participation is distributed is set from the consumer scientific discipline address. during this case, either the primary 3 octets of the IPv4 address or the full IPv6 address square measure accustomed calculate the hash price. the tactic guarantees that requests from a similar address get to a similar server unless it's not out there.
If one of the servers needs to be temporarily removed from the load‑balancing rotation, it will be marked with the down parameter so as to preserve this hashing of consumer scientific discipline addresses. Requests that were to be processed by this server square measure mechanically sent to subsequent server within the group:

    upstream backend {
    ip_hash;
    server backend1.example.com;
    server backend2.example.com;
	}


If one of the servers needs to be temporarily removed from the load‑balancing rotation, it are often marked with the down parameter so as to preserve the present hashing of consumer scientific discipline addresses. Requests that were to be processed by this server area unit mechanically sent to consequent server within the group:

    upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com down;
	}

#### <i class="icon-pencil"></i>Generic Hash

Generic Hash – The server to which a request is sent is determined from a user‑defined key which can be a text string, variable, or a mixture. for instance, the key is also a paired supply information science address and port, or a URI as during this example:

    upstream backend {
	    hash $request_uri consistent;
	    server backend1.example.com;
	    server backend2.example.com;
	}


The optional consistent parameter to the hash directive enables ketama consistent‑hash load balancing. Requests are evenly distributed across all upstream servers based on the user‑defined hashed key value. If associate degree upstream server is additional to or faraway from associate degree upstream cluster, only a few keys are remapped which minimizes cache misses in the case of load‑balancing cache servers or other applications that accumulate state.


#### <i class="icon-pencil"></i>Least Time (NGINX Plus only) 

Least Time (NGINX and only) – for every request, NGINX and selects the server with rock bottom average latency and therefore the lowest range of active connections, wherever rock bottom average latency is calculated supported that of the subsequent parameters to the least_time directive is included:

-   `header`  – Time to receive the first byte from the server
-   `last_byte`  – Time to receive the full response from the server

	    upstream backend {
	    least_time header;
	    server backend1.example.com;
	    server backend2.example.com;
		}

----------

### Footnotes


[1]

[2]

