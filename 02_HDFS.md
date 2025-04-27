## About HDFS:

![image](https://github.com/user-attachments/assets/683eca0c-d835-4c13-9e94-c079e59c7ea1)

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

![image](https://github.com/user-attachments/assets/7a24c394-a44f-4746-b73b-aaf252211a0e)


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


![image](https://github.com/user-attachments/assets/04fc069c-4bd1-431b-be72-b33eedc3a1d2)

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
![image](https://github.com/user-attachments/assets/88f8b0d1-25b3-4b14-ae2a-762756a38487)

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

![image](https://github.com/user-attachments/assets/e72fcbf9-0ee9-45c4-936b-1c582fb8c3d4)

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

![image](https://github.com/user-attachments/assets/58246c0f-3891-46b2-8b2d-f187bc77069a)


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

![image](https://github.com/user-attachments/assets/0a2e2c2c-f1b9-4187-b1d4-333a063942ac)


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

![image](https://github.com/user-attachments/assets/8829b3f4-f5da-4665-83f3-0de3e93c2660)


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

![image](https://github.com/user-attachments/assets/97bb47e9-e137-4436-b416-a20115b70297)


1. NameNode starts in read-only mode (called safemode).
2. NameNode enters read-write mode (exits safemode).

## NameNode CheckPoint Operation:

![image](https://github.com/user-attachments/assets/8c3625d7-5ac7-429e-9c84-cad0718ca6e2)

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
![image](https://github.com/user-attachments/assets/9adb3612-635c-4e96-b620-a5a9ebf26fcf)
1. Client requests to read a NameNode
file from HDFS
2. NameNode provides a
sorted list of DataNodes for
each data block
3. Client reads data block
from closest DataNode and
verifies the block’s
checksums

## The DataNode Block Reports
![image](https://github.com/user-attachments/assets/efd13284-aed8-427a-89a0-1766de3bc3c5)

## DataNode Block Reports - Detailed View

![image](https://github.com/user-attachments/assets/4b8c129e-94bf-441c-82bf-f40b5fbec3b8)

► At DataNode startup, a block report is sent
to the NameNode after 3 minutes.
► Determined by:
► dfs.blockreport.initialDelay = 120

► Updated block reports are set every 6 hours
at part of a heartbeat:
► Determined by:
► dfs.blockreport.intervalMsec =
21600000

► If the number of blocks is large, the report
is split across multiple heartbeats.
► dfs.blockreport.split.threshold =
1000000

## DataNode Failure

![image](https://github.com/user-attachments/assets/168f6ba4-eb89-43f7-812f-a63462e17810)

## DataNode Failure - Detailed View

![image](https://github.com/user-attachments/assets/4237b5e2-4a07-48ea-a6eb-de19647ac2a8)


► A NameNode listens for DataNode heartbeats to
determine availability.
► A DataNode heartbeats every 3 seconds.
► dfs.heartbeat.interval
► If heartbeats are not received, a DataNode is:
► Declared stale after 30 seconds and used last
► dfs.namenode.stale.datanode.interval
► Declared dead after 10.5 minutes and not used
► dfs.namenode.heartbeat.recheck-interval
and dfs.heartbeat.interval

► A dead DataNode forces the NameNode to re-
replicate the data blocks.

## Failed DataNode Disks

![image](https://github.com/user-attachments/assets/cad580ba-f7d1-4e4c-9d76-dce1d8120b17)

► A DataNode typically has multiple disks to:
► Enhance I/O performance
► Create more available HDFS storage space
► More disks create more opportunity for
failure.
► By default, a failed disk will cause a
DataNode to stop offering service.
► Can modify
dfs.datanode.failed.volumes.tolera
ted to make a DataNode tolerant of one or
more failed disks.
► 0 by default

## HDFS Commands

hdfs dfs –command [args]

Here are a few (of the almost 30) HDFS commands:
-cat: display file content (uncompressed)
-text: just like cat but works on compressed files
-chgrp,-chmod,-chown: changes file permissions
-put,-get,-copyFromLocal,-copyToLocal: copies files
from the local file system to the HDFS and vice versa.
-ls, -ls -R: list files/directories
-mv,-moveFromLocal,-moveToLocal: moves files
-stat: statistical info for any given file (block size, number of blocks,
file type, etc.)

To see the help of any command:

## Examples of HDFS Commands

hdfs dfs -mkdir mydata

hdfs dfs -put numbers.txt
mydata/

hdfs dfs -ls mydata

/mydata is the relative path to HOME

## HDFS File Permissions

• Files and directories have owners and groups
• r = read
• w = write
• x = permission to access the contents of a directory

![image](https://github.com/user-attachments/assets/9df616b6-0920-41d1-9fd7-6beaf8154d03)

## File and Directory Attributes

![image](https://github.com/user-attachments/assets/323ace1c-3c0c-445f-a24c-25403fdf003d)

## HDFS Permissions

| Permission | Authorized Directory Actions | Authorized File Actions |
Permission Authorized Directory Actions Authorized File Actions
r = read | View (list) directory contents | View file contents
w = write | Create or delete files or subdirectories | Write, or append to, file contents
x = execute | Access a directory | Ignored for HDFS

Permissions are
applied according
to the most
specific user class
applicable to a
user.

![image](https://github.com/user-attachments/assets/7d7f8154-aa29-45fd-9b96-21957565806d)

## HDFS Home Directories

⬢ Users and applications might have a home directory.
⬢ Home directories are used in concert with permissions to control data access.

![image](https://github.com/user-attachments/assets/41f4c2bc-3b5d-4a12-9a88-952908105245)

