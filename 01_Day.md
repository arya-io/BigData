Big Data is a problem
Hadoop is a solution for it.

Hadoop has three entities:
- Storage: Store the data.
- Cluster Resource Management: Coordinate between storage and processing.
- Processing: Analysing/processing the data.

The Storage part is known as HDFS (Hadoop Distributed File System)

Map Reduce Framework is implemented by Processing part. Implementaton is in Java Programming Language.

Map Reduce is restricted to only Java. Spark handles all tasks of Map Reduce and in more elegant way. It provides interface for different programming languages.
Spark is also a ETL Tool.

Pig Latin is a scripting language used in Pig which is an ETL Tool.
HBase is similar to MongoDB and Cassandra and is also a NoSQL Database.
But HBase is distributed NoSQL Database.
HBase cannot be installed without Hadoop. It stores the data in HDFS.
HBase native implementation is in Java.

Hive is a DataWarehouse.
Datawarehouse and Databases are different. Databases stores structured data.
Datawarehouses are designed to store historical data.
In order to store Big Data, we need to use Data Warehouses and not Databases.

Airflow is workflow management system.
Data Cleansing -> Data Transformation -> Data Analysis
e.g., Name with space -> Split first and last name -> Data Analysis

In order to do all these process in automated way, AirFlow comes into picture.
This whole thing can be achieved through Linux, Shell Scripting as well.

Kafka is a messaging system. It is a streaming platform.
Real-time Data Analytics. e.g., Uber, use of GPS System
Kafka is not used for processing data. Used for Spark streaming, which is used for real time data analytics.

---

Data Science Life Cycle:

1. Business Understanding: Ask relevant questions to the client. This is RA Phase: Requirement Analysis. There is an objective which needs to be solved. Main role is of the Domain Expert, Business Analyst.. No coding required.
2. Data Mining: Giving POC (Proof of Concept) to the client. We need to use the data. Therefore, we need to gather or scrap the data using Web Scraping. SQOOP is used here. This scraped data is raw data. It might contain NULL data and many inconsistencies. We cannot process raw data. Therefore, we do Data Cleaning.
3. Data Cleansing: Fixing the inconsistencies present in the raw data.
4. Data Exploration and Feature Engineering: Exploring, splitting, transforming the data. Select important features and construct more meaningful ones using the data you have.
5. Predictive Modelling: Machine Learning is implemented here. But first, we have to perform above steps.
6. Data Visualization: Graph the plots and extract the insights and communicate them with the stakeholders (business owners).

Processes 2, 3, 4 are known as Data Engineering.
This process can be automated using Linux and Spark.

---

Windows OS is built on Machine Windows which is known as HOST OS.
Oracle Virtual Box is built on top of Machine Windows which is known as Hypervisor. This is Guest Machine.
We have created two virtual machines: Cloudera, BigDataVM
Cloudera has CentOS Linux.
BigDataVM has Ubuntu Debian Linux.

In 99% of cases in Production Environment, we will be working with Linux.
Another environment is the Developement Environment, where we perform development and testing. BigDataVM and Cloudera which we are using are Development Environment.

---

Concept of Edit Share in Virtual Box's VM for BigDataVM:
Mount Point is a concept of Linux and not Windows.
We are accessing the folder present on the local device instead of accessing them from a remote cloud.
We have specified Windows Path in Folder Path section.

talentum@talentum-virtual-machine:~$ echo $HOME
/home/talentum
talentum@talentum-virtual-machine:~$ pwd
/home/talentum

---

We downloaded a zip file, extracted and moved that file into the BigData_Staging folder.
Now with BigDataVM, we counted the number of lines in that csv.
Then we stored that count in a new file named count.txt in the home directory.
This count.txt is then shared with the 'shared' folder.
This is now accessible in Windows (Host Machine) too.

Command for word count:

wc -l soccer_scores.csv | cat > count.txt
wc -l soccer_scores.csv > count.txt

Second process is efficient because same task is achieved by using a single process.

For copying the file, use command

cp ./count.txt ~/shared/

When file is copycommand.sh, the output is: copycommand: Bourne-Again shell script, ASCII text executable

When file is copycommand, the output is: copycommand: ASCII text

 which python (Add #!/usr/bin/python)
 Output:
 copycommand: Python script, ASCII text executable

 bash sees the metadata first (checks if it is python file or shebang script or just a normal text file).

---

Databases work on the principle of OLTP.
Data Warehouses(HIVE) are OLAP.
NoSQL Databases work on the principle of OLAP.
Hive by Facebook is a Data Warehouse.
In RDBMS, model is a table.

## Relational Empire to BigData/NoSQL

• Today, vendors unite under the NoSQL / Big Data brand
• Around 2008, triggered by Facebook’s open source versions of Hive and Cassandra,
the NoSQL counter-revolution started.
• This space gets all of the attention today.
• the modern development platforms use schema-free or semi-structured
approaches (also under the umbrella of NoSQL).
• “Model as you go” is a common theme

---

## Operational Systems vs Data Warehousing
• Traditional database systems are designed to support typical day-to-day
operations via individual user transactions (e.g. registering for a course, entering a
financial transaction, etc.).
• Such systems are generally called operational or transactional systems.
• Operational system is one source of data
• There are still different sources of data
• So heterogenous information sources is the challenge
• Does not provide integrated view
• Does not provide uniform user interface
• Does not support sharing
• Result of above challenges affects decision-making processes across the
enterprise
RDBMS is a transactional system, e.g., COMMIT and ROLLBACK.
Uniform User Interface in RDBMS will always be table or VIEW Only.
Forecasting -> Predictive Modeling
• A data warehouse complements an existing operational system by providing
forecasting and decision-making processes across the enterprise
• A data warehouse acts as a centralized repository of an organization's data,
ultimately providing a comprehensive and homogenized view of the organization.

```mermaid
mindmap
  root((Heterogeneous<br>Information Sources))
    "Heterogeneities are everywhere"
      Scientific Databases
      Different interfaces
      Different data representations
      Duplicate and inconsistent information
      Vertical fragmentation of informational systems<br>(vertical stove pipes)
      Result of application (user)-driven development<br>of operational systems
    Administrative Systems
    World Wide Web
    Digital Libraries
```

---

## What data exists in Data Warehouse?
• Large volumes of detailed data already exist in transactional database systems.
• A core subset of this data will be imported into the data warehouse, prioritized
by subject area (i.e. by business area), including finance, research, contracts and
grants, enrollment analysis, alumni, etc.
• A fundamental axiom of the data warehouse is that the imported data is
both read-only and non-volatile. • As the amount of data within the data warehouse grows, the value of the data
increases, allowing a user to perform longer-term analyses of the data.

RDBMS has operational data generally and not the historical data.

In Data Warehouse, data is read-only and non-volatile.

---

## What does a Data Warehouse do?
Integrate divergent information from various systems which enable users to quickly produce powerful ad-hoc queries and perform complex analysis
Create an infrastructure for reusing the data in numerous ways
Create an open systems environment to make useful information easily accessible to authorized users
Help managers make informed decisions


---

## Data Warehouse - Practitioners viewpoint

A data warehouse is simply a single, complete, and consistent store of data
obtained from a variety of sources and made available to end users in a way
they can understand and use it in a business context.

Schema in RDBMS is always a MetaData.

---

## DataWarehouse vs OLTP

### Enterprise Data Warehouse
Integrated Data
Current/Historical Data
Organized by Subject
Non-Volatile Data
Denormalized Data
Descriptive Data
Detailed/Summarized Data
Knowledge user (Manager)

### Traditional Database
Application-specific Data
Current Data
Organized for Data Entry
Updated Data
Normalized Data
Encoded Data
Raw Data
Clerical User

---

## Data Warehouse - OLAP:

• OLAP (Online Analytical Processing) is the technology behind many Business
Intelligence (BI) applications.
• OLAP is a powerful technology for data discovery, including capabilities for
limitless report viewing, complex analytical calculations, and predictive “what if”
scenario (budget, forecast) planning.

---

## Advantages:

• OLAP technology has been defined as the ability to achieve “fast access to shared
multidimensional information.”
• Given OLAP technology’s ability to create very fast aggregations and calculations
of underlying data sets, one can understand its usefulness in helping business
leaders make better, quicker “informed” decisions.

---

## Lesson Review:

1. State True or False - The decision support wave introduced Online
Analytical Processing (OLAP) and specialized DBMSs ?

1. Which type of system acts as a centralized repository of an organization's
data, ultimately providing a comprehensive and homogenized view of the
organization ?

1. A fundamental axiom of the data warehouse is that the imported data is
both __________ and ______________

1. State True or False - A staging area is an intermediate storage area used
for data processing during the extract, transform and load (ETL) process.

1. State any advantage of OLAP Technology

---

# Introduction to Hadoop and its ecosystem

## What makes data Big Data?
► The phrase Big Data comes from the computational
sciences
► Specifically, it is used to describe scenarios where the
volume and variety of data types overwhelm the
existing tools to store and process it
► In 2001, the industry analyst Doug Laney described Big
Data using the three V’s of volume, velocity, and
variety

---

## The Three V's of Big Data: Variety, Volume, Velocity

Variety: Unstructured and semi-structured data is becoming as strategic as the traditional structured data.
Volume: Data coming in from new sources as well as increased regulation in multiple areas means storing more data for longer periods of time.
Velocity: Machine data, as well as data coming from new sources, is being ingested at speeds not even imagined a few years ago.

---

## Variety

► Variety refers to the number of types of data being
generated
► Varieties of data include structured, semi-structured,
and unstructured data arriving from a myriad of sources
► Data can be gathered from databases, XML or JSON
files, text documents, email, video, audio, stock ticker
data, and financial transactions

► There are problems related to the variety of data. This
include
► How to gather, link, match, cleanse, and transform data across
systems.
► You also have to consider how to connect and correlate data
relationships and hierarchies in order to extract business value
from the data.

---

## Volume:
► Volume refers to the amount of data being generated.
Think in terms of gigabytes, terabytes, and petabytes
► Many systems and applications are just not able to
store, let alone ingest or process, that much data
► Many factors contribute to the increase in data volume.
This includes
► Transaction-based data stored for years
► Unstructured data streaming in from social media
► Ever increasing amounts of sensor and machine data being
produced and collected
There are problems related to the volume of data
► Storage cost is an obvious issue
SAN Storage: $2-10/GB
NAS Filers: $1-5/GB
Local Storage: $0.05/GB
► Another problem is filtering and finding relevant and valuable
information in large quantities of data that often contains not
valuable information
You also need a solution to analyze data quickly enough
in order to maximize business value today and not just
next quarter or next year

--- 

## Velocity:
Velocity refers to the rate at which new data is
created. Think in terms of megabytes per second and
gigabytes per second
► Data is streaming in at unprecedented speed and must
be dealt with in a timely manner in order to extract
maximum value from the data
► Sources of this data include logs, social media, RFID
tags, sensors, and many more

► There are problems related to the velocity of data.
These include not reacting quickly enough to benefit
from the data
► For example, data could be used to create a dashboard
that could warn of imminent failure or a security
breach
Failure to react in time could lead to service outages

► Another problem related to the velocity of data is that
data flows tend to be highly inconsistent with periodic
peaks.

► Causes include daily or seasonal changes or event-
triggered peak loads

► For example, a change in political leadership could
cause a peak in social media

---

## Hadoop Was Designed for Big Data

“Big Data is high-volume, -velocity and -variety
information assets that demand cost-effective,
innovative forms of information processing for
enhanced insight and decision making.” – Gartner

---

## Hadoop Was Designed for Big Data

► The Gartner quote makes a good point.
► It is not enough to understand what Big Data is and then collect
it
► You must also have a means of processing it in order to extract
value from it
► The good news is that Hadoop was designed to collect,
store, and analyze Big Bata
► And it does it all in a cost-effective way

---

## What is Apache Hadoop?

► So what is Apache Hadoop?
► It is a scalable, fault tolerant, open source framework for the
distributed storing and processing of large sets of data on
commodity hardware
► But what does all that mean?

---

## What is Apache Hadoop scalability?

► Well first of all it is scalable.
► Hadoop clusters can range from one machine to
thousands of machines. That is scalability!
- Hadoop administrator is responsible for storing Hadoop cluster.
- To conclude, Hadoop is a cluster based environment.
- This is a production environment.
- Creating replicas is the responsibility of the DataNode.
- How many blocks and where should those blocks go is the responsibility of the NameNode.
---

## What is Apache Hadoop fault tolerant?

► It is also fault tolerant
► Hadoop services become fault tolerant through
redundancy
► For example, the Hadoop distributed file system, called
HDFS, automatically replicates data blocks to three
separate machines, assuming that your cluster has at
least three machines in it
► Many other Hadoop services are replicated too in order
to avoid any single points of failure

1. Client sends a request to the NameNode to add a
file to HDFS
2. NameNode tells
client how and
where to distribute
the blocks
3. Client breaks the data
into blocks and writes each
block to a DataNode
4. The DataNode replicates each block to two other
DataNodes (as chosen by the NameNode)

dfs.blocksize() tells how many blocks need to be created.
Namenode is not responsible for creating the blocks. It is the job of the client.
What if a datanode gets crashed? We might lose the data.
So in order to tackle this problem, we create replicas.
But how many replicas should be created. The default value of creating replicas is 3.
These configurations are known to master node.


sudo jps
Output:
The sudo jps command is used to list all Java processes running on a system, along with their process IDs (PIDs)
The output usually includes:

Process ID (PID): The unique identifier for each running Java process.

Process name or class name: The name of the main class or process.

jps stands for Java Virtual Machine Process Status Tool

The jps command (Java Process Status tool), when run without sudo, simply lists the Java processes started by the user who executed the command. It displays the process IDs (PIDs) of Java Virtual Machines running on your machine along with their respective main class or jar names, if available.

Hadoop
 - Storage (HDFS)
    - Namenode (Master Node)
    - Datanode (Worker/Slave Node)

 Namenode and Datanode forms a cluster.
  
Master Node can only be one while Worker Nodes can be multiple.
EDGE Node is a different entity in Production environment while in Development Environment EDGE node is present in the same machine.

Configuration in Hadoop: dfs.blocksize
size (such as 128k, 512m, 1g, etc.), Or provide complete size in bytes (such as 134217728 for 128 MB).

To see the dfs.blocksize description of particular version of hadoop:
run `hadoop version` on cloudera Virtual Machine's Terminal

We will get the version of hadoop

Then visit hadoop.apache.org
Go to bottom
Then click on Release archive
Check for the version, click on it
Then click on Documentation
Go to bottom in sidebar
click on hdfs-default.xml
search for dfs.blocksize
And this is how we will get the description for it.

Same process can be followed to know about dfs.replication.
dfs.replication is contributing to fault tolerance.

In Development Environment, the replication factor is 1 because there is only one machine.

Languages like Python and Java know how to process the distributed data.
But the actual work of distribution is carried out by HDFS.


