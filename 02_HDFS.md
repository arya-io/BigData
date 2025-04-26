ls# HDFS

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

---

## Replication and Block Placement

While replicating and placing the blocks, follow two strategies:

i. Minimize write cost
ii. Maximize availability and read performance
Maximum Availability of Data means:

---

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs$
This is known as LABS_HOME

 2001  cd /home/talentum
 2002  pwd
 2003  mkdir /home/talentum/hdp/pigandhive/labs
 2004  mkdir hdp
 2005  cd hdp
 2006  mkdir pigandhive
 2007  cd pigandhive
 2008  mkdir labs
 2009  cd labs
 2010  ls
 2011  cd
 2012  ls
 2013  cd shared
 2014  ls
 2015  cd
 2016  cd /hdp/pigandhive/labs
 2017  cd /home/talentum/hdp/pigandhive/labs
 2018  pwd
 2019  mkdir demos
 2020  cd
 2021  cp shared/data/stocks.csv /home/talentum/hdp/pigandhive/labs/demos
 2022  ls
 2023  cd /home/talentum/hdp/pigandhive/labs
 2024  ls
 2025  cd demos
 2026  ls
 2027  cat stocks.csv

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ ls -lh
total 3.5M
-rwxrwx--- 1 talentum talentum 3.5M Apr 25 11:36 stocks.csv

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ head -10 stocks.csv
exchange,stock_symbol,date,stock_price_open,stock_price_high,stock_price_low,stock_price_close,stock_volume,stock_price_adj_close
NYSE,XL,2010-02-08,16.47,16.85,16.29,16.51,4793200,16.51
NYSE,XL,2010-02-05,16.38,16.55,15.91,16.46,4760900,16.46
NYSE,XL,2010-02-04,17.02,17.02,16.31,16.41,6716100,16.41
NYSE,XL,2010-02-03,17.25,17.34,17.09,17.14,2657900,17.14
NYSE,XL,2010-02-02,16.93,17.52,16.80,17.33,4282200,17.33
NYSE,XL,2010-02-01,16.75,17.09,16.64,16.88,3258200,16.88
NYSE,XL,2010-01-29,16.92,17.16,16.68,16.77,4546200,16.77
NYSE,XL,2010-01-28,17.08,17.08,16.66,16.75,4069700,16.75
NYSE,XL,2010-01-27,16.74,17.08,16.49,16.99,3339600,16.99

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ wc -l stocks.csv
65021 stocks.csv

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ ls -lh stocks.csv
-rwxrwx--- 1 talentum talentum 3.5M Apr 25 11:36 stocks.csv

## Path Mapping

| Sr. No. | HDP         | BigData                        | Cloudera                     |
|---------|-------------|--------------------------------|------------------------------|
| 1       | HDFS - Home | /user/root                    | /user/talentum              | /user/cloudera |
| 2       | LABS_HOME   | /root/hdp/pigandhive/labs     | ~/hdp/pigandhive/labs        | ~/hdp/pigandhive/labs |

3. STAGING_AREA: It is a folder on the Host machine which is mapped to mount point on Linux Virtual Machine.
talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ less stocks.csv
Press q to quit

b.Try putting the file into HDFS with a block size of 30 bytes: 

to check if hadoop is in running state
check through:

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ jps
13736 Jps

Start hadoop
talentum@talentum-virtual-machine:~$ bash Start-Hadoop-Hive.sh 

talentum@talentum-virtual-machine:~$ jps
15123 Jps
15030 RunJar
13974 NameNode
14503 ResourceManager
14649 NodeManager
14348 SecondaryNameNode
14143 DataNode

We have the csv file of 3.5 MB but as asked we have store it for 30 bytes

hdfs dfs -D dfs.blocksize=30 -put stocks.csv

if dfs.blocksize=30 is not mentioned, then it will consider it as default whose value is 128 MB

The above command got failed. To check enter:

echo $?
It will give output as 1 which means the command has got failed.

---

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs dfs -D dfs.blocksize=2000000 -put stocks.csv 
-put: Invalid values: dfs.bytes-per-checksum (=512) must divide block size (=2000000).
Usage: hadoop fs [generic options] -put [-f] [-p] [-l] <localsrc> ... <dst>

---

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs dfs -D dfs.blocksize=1048576 -put stocks.csv 
talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ echo $?
0

Namenode > namespace > metadata
Journaling will contain information that the state has been changed.
3 Blocks have been identified.
1 MB each and a block less than 1 MB.
Client will create 4 blocks and will create checksum for each.
Replication factor is 3.
Hardware requirements according to replication factor will be 1 because we have only one machine.

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs dfs -lsFound 1 items
-rw-r--r--   1 talentum supergroup    3613198 2025-04-25 12:23 stocks.csv

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ ls -lh ~/hdp/pigandhive/labs/demos/stocks.csv
-rwxrwx--- 1 talentum talentum 3.5M Apr 25 11:36 /home/talentum/hdp/pigandhive/labs/demos/stocks.csv

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ ls -lh stocks.csv
-rwxrwx--- 1 talentum talentum 3.5M Apr 25 11:36 stocks.csv

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs fsck /user/talentum/stocks.csv -files -blocks -locations
Connecting to namenode via http://localhost:50070/fsck?ugi=talentum&files=1&blocks=1&locations=1&path=%2Fuser%2Ftalentum%2Fstocks.csv
FSCK started by talentum (auth:SIMPLE) from /127.0.0.1 for path /user/talentum/stocks.csv at Fri Apr 25 12:36:53 IST 2025
/user/talentum/stocks.csv 3613198 bytes, 4 block(s):  OK
0. BP-387144675-127.0.1.1-1745562626299:blk_1073741825_1001 len=1048576 repl=1 [DatanodeInfoWithStorage[127.0.0.1:50010,DS-84a3eca0-8600-4e63-ac0f-fd37ca86c61e,DISK]]
1. BP-387144675-127.0.1.1-1745562626299:blk_1073741826_1002 len=1048576 repl=1 [DatanodeInfoWithStorage[127.0.0.1:50010,DS-84a3eca0-8600-4e63-ac0f-fd37ca86c61e,DISK]]
2. BP-387144675-127.0.1.1-1745562626299:blk_1073741827_1003 len=1048576 repl=1 [DatanodeInfoWithStorage[127.0.0.1:50010,DS-84a3eca0-8600-4e63-ac0f-fd37ca86c61e,DISK]]
3. BP-387144675-127.0.1.1-1745562626299:blk_1073741828_1004 len=467470 repl=1 [DatanodeInfoWithStorage[127.0.0.1:50010,DS-84a3eca0-8600-4e63-ac0f-fd37ca86c61e,DISK]]

Status: HEALTHY
 Total size:	3613198 B
 Total dirs:	0
 Total files:	1
 Total symlinks:		0
 Total blocks (validated):	4 (avg. block size 903299 B)
 Minimally replicated blocks:	4 (100.0 %)
 Over-replicated blocks:	0 (0.0 %)
 Under-replicated blocks:	0 (0.0 %)
 Mis-replicated blocks:		0 (0.0 %)
 Default replication factor:	1
 Average block replication:	1.0
 Corrupt blocks:		0
 Missing replicas:		0 (0.0 %)
 Number of data-nodes:		1
 Number of racks:		1
FSCK ended at Fri Apr 25 12:36:53 IST 2025 in 18 milliseconds


The filesystem under path '/user/talentum/stocks.csv' is HEALTHY

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs dfs -rm stocks.csv
25/04/25 13:02:30 INFO fs.TrashPolicyDefault: Namenode trash configuration: Deletion interval = 0 minutes, Emptier interval = 0 minutes.
Deleted stocks.csv
talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs dfs -ls
talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs dfs -put stocks.csv 
25/04/25 13:03:57 WARN hdfs.DFSClient: Caught exception 
java.lang.InterruptedException
	at java.lang.Object.wait(Native Method)
	at java.lang.Thread.join(Thread.java:1257)
	at java.lang.Thread.join(Thread.java:1331)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeResponder(DFSOutputStream.java:609)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.closeInternal(DFSOutputStream.java:577)
	at org.apache.hadoop.hdfs.DFSOutputStream$DataStreamer.run(DFSOutputStream.java:573)

talentum@talentum-virtual-machine:~/hdp/pigandhive/labs/demos$ hdfs fsck /user/talentum/stocks.csv -files -blocks -locations
Connecting to namenode via http://localhost:50070/fsck?ugi=talentum&files=1&blocks=1&locations=1&path=%2Fuser%2Ftalentum%2Fstocks.csv
FSCK started by talentum (auth:SIMPLE) from /127.0.0.1 for path /user/talentum/stocks.csv at Fri Apr 25 13:08:44 IST 2025
/user/talentum/stocks.csv 3613198 bytes, 1 block(s):  OK
0. BP-387144675-127.0.1.1-1745562626299:blk_1073741829_1005 len=3613198 repl=1 [DatanodeInfoWithStorage[127.0.0.1:50010,DS-84a3eca0-8600-4e63-ac0f-fd37ca86c61e,DISK]]

Status: HEALTHY
 Total size:	3613198 B
 Total dirs:	0
 Total files:	1
 Total symlinks:		0
 Total blocks (validated):	1 (avg. block size 3613198 B)
 Minimally replicated blocks:	1 (100.0 %)
 Over-replicated blocks:	0 (0.0 %)
 Under-replicated blocks:	0 (0.0 %)
 Mis-replicated blocks:		0 (0.0 %)
 Default replication factor:	1
 Average block replication:	1.0
 Corrupt blocks:		0
 Missing replicas:		0 (0.0 %)
 Number of data-nodes:		1
 Number of racks:		1
FSCK ended at Fri Apr 25 13:08:44 IST 2025 in 0 milliseconds


The filesystem under path '/user/talentum/stocks.csv' is HEALTHY

---

If we want to see any datablock, we will have to connect through edge node:

Copy the block name

ssh {ipAddress}
ssh resourcemanager
---

## Persisting File System Information on the NameNode

► File system state
is maintained and
served from
memory.
► Memory is fast but
volatile.
► File system state
is regularly
persisted to disk.

---

## The NameNode Startup

1. When the NameNode starts, it reads
the fsimage_N and edits_N files.
1. The transactions in edits_N are
merged with fsimage_N. 1. A newly created fsimage_N+1 is
written to disk, and a new, empty
edits_N+1 is created.

The NamdeNode will be in safemode, a read-only mode.

4. Now a client application can
create a new file in HDFS
4. The NameNode journals that
create transaction in the
edits_N+1 file

---
We are running this on cloudera

sudo find / -type f -name hdfs-site.xml
specify name after `-name`
specify filetype after `-type`, here we have used `f`
`sudo` works as a root user
`/` for root directory


Open a new terminal
Search for that file using that path
dfs.namenode.name.dir

hdfs -site

There are configuration files for each component of Hadoop:
HDFS
YARN
MapReduce

These files (site.xml) are very sensitive.

---

hdfs dfsadmin
hdfs dfsadmin -help safemode

## NameNode StartUp - Detailed View

1. NameNode starts in read-only mode (called safemode).
2. NameNode enters read-write mode (exits safemode).

## NameNode CheckPoint Operation:
• NameNodes must periodically perform a checkpoint
operation or the edits file would continue to grow
without bounds. • A checkpoint operation merges the changes recorded in
the current edits file with the information in the current
fsimage file, and then replaces the edits and fsimage
files with a new files. • The new edits file will initially be empty

1. Primary creates and uses
new edits file
1. Secondary/Standby
retrieves edits and
fsimage files
1. The edits and fsimage
files merged in memory
1. New fsimage created
1. New fsimage sent to
Primary
1. Primary saves new
fsimage and continues
using new edits file

## Reading Data

## The DataNode Block Reports

## DataNode Block Reports - Detailed View

## DataNode Failure

## DataNode Failure - Detailed View

## Failed DataNode Disks

## HDFS Commands

To see the help of any commandhd

## Examples of HDFS Commands

/mydata is the relative path to HOME

## HDFS File Permissions

## File and Directory Attributes

## HDFS Permissions

## HDFS Home Directories












