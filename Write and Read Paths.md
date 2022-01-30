# Cassandra Paths

Let's understand write and read paths in Cassandra

[Write Path](write-path)
[Read Path](read-path)

## Write Path

Cassandra runs on JVM. It has access to the memory (MemTable) and the physical storage/disk  (Commit Log). When a write is requested by the client, Cassandra writes the data to both the `Commit Log` and `MemTable`. The difference is: `Commit Log` table doesn't have the sorted order of data based on the clustering index, but the MemTable does have the sorted order as it can be seen in the image below.

![Write01](paths/Write01.png)

When MemTable and CommitLog grow as the data is written, MemTable data gets flused to an immutable table, called `SS Table` on the disk. Both MemTable and CommitLog get flushed and this same process continues. In the end, there are a lot of SS Tables on the disk, which also get combined into a few SS tables using the process called `Compaction`.

![Write02](paths/Write02.png)

![Write03](paths/Write03.png)

![Write04](paths/Write04.png)


## Read Path

As you can see, the data is in multiple places as below. The data from MemTable is newer so the data will be returned from MemTable, if the same key exists but older data in other tables.

![Read01](paths/Read01.png)

