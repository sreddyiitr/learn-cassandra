# learn-cassandra
Cassandra Basics

*The primary key is the unique combination of the partition key and all clustering columns for that row in the table. The partition key does not need to be unique.*

*Materialized Views help to query data based on non-primary key columns and eliminates the need for secondary indexes. Seconday Index is most expensive in cassandra because the data needs to be queried from multiple tables in a cluster*
  *Cassandra is repsonsible for updating MV with the data from base tables*
    *Drawback: Expect a small performance hit on writes to keep MVs in sync*
