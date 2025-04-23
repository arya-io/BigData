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
Another environment is the Developer Environment.

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

## Operational Systems vs Data Warehousing
RDBMS is a transactional system, e.g., COMMIT and ROLLBACK.
Uniform User Interface in RDBMS will always be table or VIEW Only.
Forecasting -> Predictive Modeling

## What data exists in Data Warehouse?

RDBMS has operational data generally and not the historical data.

In Data Warehouse, data is read-only and non-volatile.

## What does a Data Warehouse do?

## Data Warehouse - Practitioners viewpoint

Schema in RDBMS is always a MetaData.

## DataWarehouse vs OLTP

## Data Warehouse - OLAP

## Advantages

## Lesson Review

---

# Introduction to Hadoop and its ecosystem

## What makes data Big Data?
## The Three V's of Big Data: Variety, Volume, Velocity

Variety: Unstructured and semi-structured data is becoming as strategic as the traditional structured data.
Volume: Data coming in from new sources as well as increased regulation in multiple areas means storing more data for longer periods of time.
Velocity: Machine data, as well as data coming from new sources, is being ingested at speeds not even imagined a few years ago.

## Variety
## Volume:
SAN (Storage As A Network)
## Velocity

