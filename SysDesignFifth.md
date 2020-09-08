#  MySQL Replication

Introduction


### Replication Scheme

https://severalnines.com/resources/tutorials/mysql-replication-high-availability-tutorial


#### <i class="icon-file"></i> Asynchronous replication

MySQL Replication by default is asynchronous. this can be the oldest, hottest and wide deployed replication theme. With asynchronous replication, the master writes events to its binary log and slaves request them once they square measure prepared. there's no guarantee that any event can ever reach any slave. It’s a loosely coupled master-slave relationship, where:

-   Master does not wait for Slave
-   Slave determines how much to read and from which point in the binary log
-   Slave can be arbitrarily behind master in reading and applying changes


If the master crashes, transactions that it's committed may not are transmitted to any slave. Consequently, failover from master to slave during this case might end in failover to a server that's missing transactions relative to the master.

Asynchronous replication provides lower write latency, since a write is acknowledged regionally by a master before being written to slaves. it's nice for browse scaling as adding a lot of replicas doesn't impact replication latency. sensible use cases for asynchronous replication embody readying of browse replicas for browse scaling, live backup copy for disaster recovery and analytics/reporting.


#### <i class="icon-pencil"></i> Semi-synchronous Replication

MySQL conjointly supports semi-synchronous replication, wherever the master doesn't ensure transactions to the consumer till a minimum of one slave has derived the amendment to its relay log, and flushed it to disk. To modify semi-synchronous replication, further steps for plugin installation square measure needed, and should be enabled on the selected MySQL master and slave.

Semi-synchronous appears to be smart and sensible resolution for several cases wherever high handiness and no data-loss is vital. however you ought to take into account that semi-synchronous contains a performance impact thanks to the extra trip and doesn't give robust guarantees against knowledge loss. once a commit returns with success, it's famous that the info exists in a minimum of 2 places (on the master and a minimum of one slave). If the master commits however a crash happens whereas the master is expecting acknowledgment from a slave, it's doable that the dealings might not have reached any slave.

A good use case for semi-synchronous replication could be a backup master to cut back the impact of a master failure by minimizing the chance of information loss. We’ll justify this in details beneath ‘Chapter three - Topology for MySQL Replication’.

#### <i class="icon-trash"></i> 


#### <i class="icon-hdd"></i>

----------
### Footnotes

[1] http://www.haproxy.org/
[2]
