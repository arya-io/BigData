# HDFS

## About HDFS:

Conversation between Hadoop Client and HDFS
Hadoop Client: “I have a 200 TB
file that I need to
store.”
HDFS: “Wow! That is big
data! I will need to
distribute that across
a cluster.”
Hadoop Client: “Sounds risky!
What happens if a
drive fails?”
HDFS: “No need to worry! I
am designed for
failover.”

---

## Hadoop RDBMS:
• Assumes a task will require reading
a significant amount of data off of
a disk
• Does not maintain any data
structure
• Simply reads the entire file
• Scales well (increase the cluster
size to decrease the read time of
each task)
  - 2,000 blocks of size 256MB
  - 1.9 seconds of disk read
for each block
  - On a 40 node cluster with
eight disks on each node,
it would take about 14
seconds to read the entire
500 GB
• Uses indexes to avoid reading an
entire file (very fast lookups)
• Maintains a data structure in order
to provide a fast execution layer
• Works well as long as the index fits
in RAM

500 GB data file: 61 minutes to read this
data off of a disk (assuming
a transfer rate of 1,030
Mbps)

To check this data transfer speed, we can check this on the following website:
https://www.calctool.org/other/data-transfer

For 500 GB of data, it is saying the time required for data transfer will be 64 min 43 secs.

---

## HDFS Characterisitcs

- Hierarchical: Directories containing files are arranged in a series of parent-child relationships.
- Distributed: File system storage spans multiple drives and hosts.
- Replicated: The file system automatically maintains multiple copies of data blocks.
- Write-once, read-many optimized: The file system is designed to write data once but read
the data multiple times. Linux is write-many and read-many.
- Sequential access: The file system is designed for large sequential writes and reads.
- Multiple readers: Multiple HDFS clients may read data at the same time.
- Single writer: To protect file system integrity, only a single writer at a time is allowed.
- Append-only: Files may be appended, but existing data not updated.

## HDFS Components - NameNode and DataNodes Introduction

⬢ NameNode: Master node maintaining file system namespace and metadata including:
► File names
► Directory names
► File system hierarchy
► Permissions and ownerships
► Last modification times
► ACLs (Access Control Lists)
⬢ DataNode: Worker nodes containing only file data blocks.

## HDFS Components
NameNode
• Is the “master” node of HDFS
• Determines and maintains how the chunks of data are
distributed across the DataNodes

DataNode
• Stores the chunks of data, and is responsible for replicating
the chunks across other DataNodes

## HDFS Architecture

The NameNode
and DataNodes
are daemons
running in a Java
virtual machine.

Primary NameNode
Namespace
• Hierarchy
• Directory names
• File names

Metadata
• Permissions and ownership
• ACLs
• Block size and replication level
• Access and last modification
times
• User quotas

memory-based service:
Journaling
• Safely records file system changes

Block Map:
- File names > block IDs

This entire information is being stored in the memory.

Secondary/Standby NameNode:
Checkpointing
• Merges the disk-based
files used to persist
in-memory file system
state information

DataNode:
They actually hold the blocks.

---

1. Client sends a request
to the NameNode to add a
file to HDFS
Big Data -> NameNode

2. NameNode tells client
how and where to
distribute the blocks
NameNode -> Big Data

3. Client breaks the data into blocks
and writes each block to a DataNode

4. The DataNode replicates each block to two other DataNodes (as
chosen by the NameNode)

---

## Writing to HDFS Storage – Detailed view

1. Client requests to write file to HDFS
2. NameNode provides a lease
to the file name
3. Client requests, for every
data block, block IDs and list
of DataNodes
4. NameNode sends block IDs,
and list of DataNodes for
each.
5. For each block, write data and checksums
to first DataNode in the list
6 & 7. Each DataNode replicates to next
DataNode, establishing a data pipeline
8. Last DataNode re-
computes and verify the checksums.
9 and 10 are acknowledgments.
11. Send ack back to client.

What is Checksum?

