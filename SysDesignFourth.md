#  MySQL Load Balancing

Introduction


### MySQL Load Balancing with HAProxy

https://severalnines.com/resources/tutorials/mysql-load-balancing-haproxy-tutorial


#### <i class="icon-file"></i> What is HAProxy

![enter image description here](https://severalnines.com/sites/default/files/resources/tutorials/mysql-load-balancing-with-haproxy-tutorial/image00.png)

HAProxy stands for prime convenience Proxy, and could be a nice software-based TCP/HTTP load balancer. It distributes a employment across a collection of servers to maximise performance and optimize resource usage. HAProxy engineered with refined and customizable health checks strategies, permitting variety of services to be load balanced in a very single running instance.

A front-end application that depends on a information backend will simply over-saturate the information with too several cooccurring running connections. HAProxy provides queuing and asphyxiation of connections towards one or additional MySQL Servers and prevents one server from changing into full with too several requests. All shoppers connect with the HAProxy instance, and also the reverse proxy forwards the affiliation to 1 of the obtainable MySQL Servers supported the load-balancing rule used.

One potential setup is to put in associate degree HAProxy on every net server (or application server creating requests on the database). This works fine if there ar solely many net servers, therefore because the load introduced by the health checks is unbroken under control. the online server would hook up with the native HAProxy (e.g. creating a mysql association on 127.0.0.1:3306), and might access all the info servers. the online and HAProxy along forms a operating unit, that the net server won't work if the HAProxy isn't obtainable.

#### <i class="icon-pencil"></i> Configuration

[Starter guide in HTML](http://cbonte.github.io/haproxy-dconv/1.9/intro.html)

[Configuration Manual in HTML](http://cbonte.github.io/haproxy-dconv/1.9/configuration.html)

#### <i class="icon-trash"></i> 


#### <i class="icon-hdd"></i>


----------

### Database Load Balancing for MySQL and MariaDB with ProxySQL

https://severalnines.com/resources/tutorials/proxysql-tutorial-mysql-mariadb


#### <i class="icon-trash"></i> ProxySQL Internals
![enter image description here](http://severalnines.com/sites/default/files/resources/tutorials/proxysql-tutorial-mysql-mariadb/image7.jpg)

ProxySQL, once started, instantly spawns a brand new method - the parent method works as associate angel method and restarts ProxySQL inside milliseconds of a crash. If you're aware of MySQL, this is often fairly just like mysqld_safe. By default, ProxySQL wants 2 ports: 6033, on that it listens for traffic and 6032, that works as a entry for managing ProxySQL. The statement admin interface will be accessed by a MySQL consumer - the bulk of the configuration is completed victimization SQL. even supposing the underlying info that ProxySQL uses to store its configuration is SQLite, an attempt was place into creating the expertise as about to MySQL as attainable. you'll be able to use a number of the MySQL syntax to examine the ProxySQL configuration (SHOW international VARIABLES) or set a brand new one (SET international variable_name = value). The backend configuration is hold on in tables - all changes area unit created through SQL: INSERT, UPDATE, DELETE.

let’s get some ideas on however ProxySQL might be utilized in your infrastructure. because it understands SQL traffic, it will do in depth routing - you'll be able to match queries by varied attributes: schema, user, host, port or maybe regular expression. this offers you a good deal of flexibility relating to that question you wish to form changes to. There’s quite a spectacular list of actions that may be taken on a question . you'll be able to cache it for an outlined quantity of your time (TTL), that reduces question latency. This additionally eliminates the requirement for external caching layer, that sometimes introduces extra quality within the application because it must manage the cache. it's additionally a way higher answer than the MySQL question cache (which, finally, has been removed in eight.0). you'll be able to additionally throttle - does one have a significant query that affects performance? you'll be able to have it run no more than, say, once per second or once per minute - it’s absolutely customizable. Another feature is question mirroring. this can be not a production-ready feature, and don’t expect to ascertain all of your traffic reflected. however beneath sure circumstances, this could be terribly helpful - for a given question, you'll be able to send it not solely to your production hosts however additionally to a separate location - to capture it within the slow log or to try and do some debugging. question re-writing permits you to rewrite a question on the fly. have you ever been during a scenario wherever straightforward FORCE INDEX would solve your issue, however you couldn’t add it while not surfing a long method to change the app, test it, roll new code etc? currently it's attainable to rewrite a question in ProxySQL and e.g., add index hints.

-   [proxysql documentation](http://www.proxysql.com/documentation)

#### <i class="icon-hdd"></i> Installing ProxySQL in ClusterControl

ClusterControl has had support for ProxySQL since version one.4.0 - it not solely installs it however an in depth UI is offered for configuration and management. during this chapter, we tend to area unit aiming to show you the way to deploy ProxySQL from inside ClusterControl and what high-availability choices area unit on the market. In next chapter, we are going to discuss additional in-depth management of the ProxySQL victimisation ClusterControl. Let’s start with the installation.

----------
### Footnotes

[1] http://www.haproxy.org/
[2]
