# Learn Cassandra 

## Cassandra Basics

* The primary key is the unique combination of the partition key and all clustering columns for that row in the table. The partition key does not need to be unique.
* Cassandra is optimized for writes first approach which means that the write path will often be more performant than the read path.


### Materialized Views ###

* Materialized Views help to query data based on non-primary key columns and eliminates the need for secondary indexes. Seconday Index is most expensive in cassandra because the data needs to be queried from multiple tables in a cluster
   * MV should contain ALL primary key columns from the base table and any non-key columns that you want to includ
   * Cassandra is repsonsible for updating MV with the data from base tables
   * Drawback: Expect a small performance hit on writes to keep MVs in sync

### Peer to Peer archirecture ###
Cassandra follows peer to peer architecture. The requests are received the the coordinator node and then routes the requests to the node that has the data based on the replication factor. Each node serves as Coordinator node and no node is lesser than the other node (unlike leader-follower or master-slave architecture)

### Gossip Protocol ###
Cassandra uses a gossip protocol for peer to peer communication between nodes on our cluster. The gossip sessions run on a periodic schedule and each node communicates with several other nodes in the cluster to share its metadata. This allows all nodes on the cluster to be aware of the overall state of the cluster as a whole and the state of other specific nodes.

Metadata can be **Heartbeat State** and **Application State**. Heartbeat State: Timestamp... Application State: Status, DC, Rack, Schema, Load, IO Pressure

### Snitch ###

* Snitch config can be found in cassandra.yaml 

* The snitch determines which datacenters and racks nodes belong to. They inform Cassandra about the network topology so that requests are routed efficiently and allows Cassandra to distribute replicas by grouping machines into datacenters and racks. 

* There are many different types of snitches available such as the simple snitch, property file snitch, Gossipping property file snith, and cloud specific snitches. Can be found in 

* Each node has the config file that holds Data Center/Region and the rack details. Nodes talk to each other using gossip protocol and gets the information about all the nodes in a cluster

* Another snitch: Dynamic snitch monitors the performance of all nodes and determines what node to use for better performance
