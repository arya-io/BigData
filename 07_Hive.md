# 🐝 Topics to be Covered in Hive  

## 🔍 Introduction to Hive
- **About Hive** – Understanding the fundamentals of Apache Hive.
- **Comparing Hive to SQL** – Key similarities and differences between Hive and traditional SQL.

## 🏗️ Hive Architecture & Querying
- **Hive Architecture** – Exploring how Hive processes queries and stores data.
- **Submitting Hive Queries** – How to write and execute queries efficiently.

## 📂 Working with Tables & Data  
- **Defining Tables** – Creating and structuring tables in Hive.
- **Loading Data into Hive** – Different ways to insert and manage data.
- **Performing Queries** – Querying data using Hive’s syntax.

## 🛠️ Labs & Demos  
- **Lab: Understanding Hive Tables** – Practical exercise on creating and managing tables.
- **Hive Partitions, Buckets, and Skewed Data** – Methods to organize large datasets efficiently.
- **Demo: Understanding Partitions and Skew** – Hands-on understanding of data distribution in Hive.
- **Sorting Data** – Techniques to order data properly for analysis.

## 🔎 Advanced Hive Techniques  
- **Lab: Analyzing Big Data with Hive** – Exploring how Hive handles large datasets.
- **Hive Join Strategies** – Optimizing joins for performance and scalability.
- **Demo: Computing ngrams** – Understanding ngram computations with Hive.
- **Lab: Joining Datasets in Hive** – Hands-on learning about dataset joins.
- **Lab: Computing ngrams of Emails in Avro Format** – Working with structured Avro data.

---

### 🐝 About Hive  

![image](https://github.com/user-attachments/assets/5de92de5-4135-451e-94bd-edde35b1cd89)

The image visually represents **Hive's ability to store and query data** from multiple sources, such as **Operational/MPP databases, Weblogs, Mobile data, and Sensor data**. It emphasizes that Hive enables users to work with familiar **SQL tools and processes**, making data analysis more accessible.

---

# 🐝 About Hive – Continued  

### 🏢 **Hive as a Data Warehouse System**  
Hive is a **data warehouse** solution built on top of **Hadoop**, designed to process and manage large-scale structured data efficiently. Think of it as a tool that **organizes and queries massive datasets** just like a traditional SQL-based database.  

### 📂 **Metadata Management**  
Hive **maintains metadata** (information about data structure) for your **big data stored in HDFS**. This metadata includes details about:
- **Table names**
- **Column types**
- **Data locations**  
Just like how a library catalog keeps track of book locations, Hive keeps track of where different pieces of data reside in Hadoop’s ecosystem.  

### 📊 **Big Data as Tables**  
Even though Hadoop stores data in files and directories, Hive **abstracts** that data into **tables**, making it easier to work with. You can think of Hive like a translator—it converts raw distributed data into a table-like format, allowing users to perform **structured queries** just as they would in a traditional database.  

### 📝 **SQL-like Operations with HiveQL**  
Hive uses **HiveQL**, a special query language that is **similar to SQL**. This means users can write queries almost the same way they would in a **relational database**, making it easy for beginners who are already familiar with SQL concepts.  
For example:  

```sql
SELECT name, age FROM employees WHERE age > 30;
```  

This HiveQL query selects employee names and ages where the age is greater than 30—just like in SQL!  

---

# 🔄 Hive's Alignment with SQL  

### 🗂️ **SQL Datatypes in Hive**  
Hive supports a variety of **SQL-like datatypes**, making it easier for users familiar with SQL to work with Hive seamlessly. Here’s a comparison of common SQL datatypes used in Hive:  

| **SQL Datatype**  | **Equivalent in Hive** |
|------------------|---------------------|
| INT | Integer values |
| TINYINT / SMALLINT / BIGINT | Different sizes of integer values |
| BOOLEAN | True/False values |
| FLOAT / DOUBLE | Decimal numbers |
| STRING / BINARY | Text and binary data |
| TIMESTAMP | Date and time values |
| ARRAY / MAP / STRUCT / UNION | Complex data types |
| DECIMAL | Precision-based decimal values |
| CHAR / VARCHAR | Fixed-length and variable-length text |
| DATE | Stores only date information |

👉 **Example:**  
```sql
CREATE TABLE employee (
    id INT,
    name STRING,
    salary DECIMAL(10,2),
    joining_date DATE
);
```
This Hive table definition follows SQL-like structure, making it intuitive for SQL users!  

---

### ⚙️ **SQL Semantics in Hive**  
Hive also supports **SQL-like semantics**, allowing users to write queries in a familiar format. Here are some key **SQL operations** that work in Hive:  

✔ **Basic Queries**  
- `SELECT` – Fetch data from tables  
- `LOAD` – Import external data into Hive  
- `INSERT` – Insert new records into tables  

✔ **Filtering & Grouping**  
- `WHERE` / `HAVING` – Apply conditions on queries  
- `GROUP BY` – Group data based on specific columns  
- `ORDER BY` / `SORT BY` – Arrange data in a specific order  

✔ **Advanced Querying**  
- `JOIN` (LEFT, RIGHT, FULL OUTER, CROSS JOIN) – Combine data from multiple tables  
- `CLUSTER BY` / `DISTRIBUTE BY` – Efficiently distribute data in Hive  
- `SUBQUERIES` – Use queries inside queries (`IN`, `EXISTS`)  
- `WINDOWING FUNCTIONS` (`RANK`, `OVER()`) – Perform analytical operations  

👉 **Example:**  
```sql
SELECT name, salary FROM employee WHERE salary > 50000 ORDER BY salary DESC;
```
This query fetches employee names with salaries above 50,000, sorted in descending order—exactly like SQL!  

---

### 📷 **Visual Reference**  
The image provides a **clear comparison between SQL Datatypes and SQL Semantics in Hive**, showing how SQL functionality is adapted in Hive for big data processing. It highlights **compatibility and ease of transition** for SQL users moving to Hive.  

---

Here's your beginner-friendly explanation of Hive, structured for clarity and easy learning! 🚀📚  

---

# 🐝 Hive  

![image](https://github.com/user-attachments/assets/ed6240e7-a921-4275-932c-e97f0376e53b)


### 🏗️ **What is Hive?**  
Apache Hive is a **data warehouse system** built on top of **Hadoop**. It is used to store, manage, and query large datasets using a **SQL-like language called HiveQL**. Instead of manually writing complex **MapReduce** programs, Hive simplifies big data analysis with structured queries.  

### 🔍 **How Hive Works**  
When you execute a query in Hive:  
1. You submit an **SQL-like query** using **HiveQL**.  
2. Hive translates it into a **MapReduce job** that runs on **Hadoop**.  
3. The result is processed and returned to the user in **tabular form**, just like a traditional database system.  

### 🛠️ **Hive Components**  
Hive works through several core components:  

| **Component** | **Function** |
|--------------|-------------|
| **HiveServer2** | Manages query execution and client requests |
| **Metastore** | Stores metadata (table structures, partitions, data locations) |
| **Compiler & Optimizer** | Converts queries into execution plans |
| **Executor** | Runs queries by translating them into Hadoop tasks |

---

### 📷 **Visual Representation**  
The image you uploaded illustrates **Hive's workflow**, showing how queries move through different components before executing as **MapReduce jobs** on Hadoop. It highlights the interactions between **HiveServer2, Metastore, Hadoop YARN, and the query optimization process**.  

---


# 📝 **Submitting Hive Queries**  

### 🖥️ **Hive CLI (Command Line Interface)**  
The **Hive CLI** is the **traditional way** to interact with Hive. It functions as a **thick client**, meaning it connects directly to the Hive service and executes queries locally.  

#### ✅ **How to Use Hive CLI**  
- Open the terminal and type:  
  ```bash
  $ hive
  ```
- This starts the Hive command-line interface, and you’ll see the prompt:  
  ```bash
  hive>
  ```
- You can now type queries directly into Hive.  

👉 **Example Query:**  
```sql
SELECT * FROM employees LIMIT 10;
```
This retrieves the first 10 records from the `employees` table.  

---

### 🌐 **Beeline (New Hive Client)**  
Beeline is a **newer, lightweight command-line client** designed to connect to **HiveServer2** instead of running locally. Unlike Hive CLI, it allows multiple users to connect remotely using **JDBC** (Java Database Connectivity).  

#### ✅ **How to Use Beeline**  
- Open the terminal and type:  
  ```bash
  $ beeline -u url -n username -p password
  ```
- This connects to a **HiveServer2 instance** with the given credentials.  
- Once connected, you can execute queries using the `beeline>` prompt.  

👉 **Example Query:**  
```sql
SELECT COUNT(*) FROM sales_data;
```
This counts the total number of rows in the `sales_data` table.  

---


# 🏗️ **Defining a Hive-Managed Table**  

### 📌 **What is a Hive-Managed Table?**  
A **Hive-managed table** (also known as an **internal table**) is a table where Hive **manages both the metadata and the actual data**. When you create a managed table, Hive **stores the data in a specific location in HDFS**, and **deleting the table removes both the metadata and the data**.  

---

### 📝 **Table Definition in Hive**  

Here's the standard way to define a **Hive-managed table**:  

```sql
CREATE TABLE customer (
    customerID INT,
    firstName STRING,
    lastName STRING,
    birthday TIMESTAMP
) ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

#### 🛠️ **Breaking it Down:**  
✔ **CREATE TABLE customer** → Defines a new table named `customer`.  
✔ **customerID INT** → Integer column for storing customer IDs.  
✔ **firstName STRING** → Text-based column for first names.  
✔ **lastName STRING** → Text-based column for last names.  
✔ **birthday TIMESTAMP** → Stores date and time information.  
✔ **ROW FORMAT DELIMITED** → Specifies the data format.  
✔ **FIELDS TERMINATED BY ','** → Defines `comma` as the separator between values.  

---

### 🎯 **Example Data for This Table**  
Imagine you have a CSV file with customer data formatted like this:  

```csv
101,John,Doe,1990-05-21 12:34:56  
102,Jane,Smith,1992-08-15 09:30:00  
103,Sam,Johnson,1988-11-03 14:00:30  
```

When this data is loaded into Hive, it will be structured into a table format, making it **easy to query and analyze**.  

---


# 🏗️ **Defining an External Table in Hive**  

### 📌 **What is an External Table?**  
An **external table** in Hive allows users to store data **outside** of Hive’s managed storage system. Unlike **managed tables**, where Hive **deletes the data when the table is dropped**, external tables **preserve the data** even if the table is removed.  

### 📝 **Creating an External Table**  

```sql
CREATE EXTERNAL TABLE salaries (
    gender STRING,
    age INT,
    salary DOUBLE,
    zip INT
) ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';
```

#### 🛠️ **Breaking it Down:**  
✔ **CREATE EXTERNAL TABLE salaries** → Defines an external table named `salaries`.  
✔ **gender STRING** → Stores gender as text.  
✔ **age INT** → Stores numerical age values.  
✔ **salary DOUBLE** → Stores salary with decimal precision.  
✔ **zip INT** → Stores zip codes as integer values.  
✔ **ROW FORMAT DELIMITED** → Specifies that fields are **separated** using a delimiter.  
✔ **FIELDS TERMINATED BY ','** → Defines `comma` as the separator between values.  

---

### 📂 **Defining a Table LOCATION**  

Sometimes, you may need to store the data in **a specific location** in HDFS while still using an external table. This ensures that Hive **references** the existing data **without moving** it to Hive’s default warehouse directory.  

```sql
CREATE EXTERNAL TABLE salaries (
    gender STRING,
    age INT,
    salary DOUBLE,
    zip INT
) ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
LOCATION '/user/train/salaries/';
```

✔ **LOCATION '/user/train/salaries/'** → Specifies where the data is physically stored in HDFS.  

💡 **Key Difference:**  
- **Internal Table:** Hive **manages** data storage. If you drop the table, the data is deleted.  
- **External Table:** Hive **only tracks metadata** while the actual data stays in its HDFS location, even if the table is removed.  

---

### 🔍 **How to Identify a Managed vs. External Table in Hive?**
You can check whether a table is **managed or external** using these methods:

#### ✅ **1. Check Table Type using `DESCRIBE FORMATTED`**
```sql
DESCRIBE FORMATTED your_table_name;
```
- Look for the **Table Type** in the output:
  - If it says **MANAGED**, it’s a **Managed Table**.
  - If it says **EXTERNAL**, it’s an **External Table**.

#### ✅ **2. Check Table Definition using `SHOW CREATE TABLE`**
```sql
SHOW CREATE TABLE your_table_name;
```
- If the output contains **EXTERNAL** in the table definition, it’s an **External Table**.
- If there’s **no EXTERNAL keyword**, it’s a **Managed Table**.

#### ✅ **3. Check Table Location using `DESCRIBE FORMATTED`**
```sql
DESCRIBE FORMATTED your_table_name;
```
- **Managed Tables** are stored in `/user/hive/warehouse/`.
- **External Tables** have a different storage path, often explicitly defined.

#### ✅ **4. Try Dropping the Table (Be Careful!)**
⚠️ **Warning:** This will remove the table, so **only use on test tables**!

```sql
DROP TABLE table_name;
```
- If **data disappears**, it was a **Managed Table**.
- If **only metadata disappears but data stays**, it was an **External Table**.

---

### 🎯 **Final Quick Summary**
| Feature            | Managed Table               | External Table              |
|--------------------|---------------------------|-----------------------------|
| **Storage location** | Hive warehouse (`/user/hive/warehouse/`) | Custom location (e.g., HDFS, S3) |
| **Data management** | Hive **manages** both data & metadata | Hive **only manages** metadata |
| **Data deletion on `DROP TABLE`** | ❌ Data **is deleted** | ✅ Data **remains** |
| **Use cases** | Temporary, intermediate, Hive-managed data | Persistent, shared, or external datasets |

---

# 📥 **Loading Data into Hive**  

Once tables are defined, you need to **load** data into Hive for querying. There are **two ways** to load data:  

### 🚀 **Loading Local Data into Hive**  

```sql
LOAD DATA LOCAL INPATH '/tmp/customers.csv'
OVERWRITE INTO TABLE customers;
```
✔ **LOCAL INPATH** → Loads data from a local file system.  
✔ **OVERWRITE INTO TABLE customers** → Overwrites existing data in the `customers` table.  

### 🌍 **Loading Data from HDFS**  

```sql
LOAD DATA INPATH '/user/train/customers.csv'
OVERWRITE INTO TABLE customers;
```
✔ **INPATH** → Loads data from HDFS instead of the local machine.  
✔ **OVERWRITE INTO TABLE customers** → Replaces existing records in Hive with new data from HDFS.  

### 🔄 **Inserting Data via Queries**  

You can also **insert data** into a table **from another table** using SQL queries:  

```sql
INSERT INTO TABLE birthdays
SELECT firstName, lastName, birthday
FROM customers
WHERE birthday IS NOT NULL;
```
✔ Selects first name, last name, and birthday from `customers` **where birthday exists**, and inserts the data into the `birthdays` table.  

---

# 🔍 **Performing Queries in Hive**  

Once data is loaded, you can start querying the tables just like **SQL databases**!  

### 📊 **Fetching All Data**  

```sql
SELECT * FROM customers;
```
✔ Returns **all columns and rows** from the `customers` table.  

### 🎯 **Filtering & Sorting Data**  

```sql
FROM customers
SELECT firstName, lastName, address, zip
WHERE orderID > 0
ORDER BY zip;
```
✔ Filters customers **where orderID is greater than 0** and sorts results by `zip`.  

### 🔗 **Joining Tables**  

```sql
SELECT customers.*, orders.*
FROM customers
JOIN orders ON (customers.customerID = orders.customerID);
```
✔ Joins `customers` and `orders` tables **based on matching customer IDs**, combining data from both tables.  

---

# 🛠️ Hive Configuration & Metastore Connection  

### 🔍 Finding the Hive Configuration File  
To locate the Hive **configuration file** (`hive-site.xml`), use the following command:  
```bash
sudo find / -type f -name hive-site.xml
```
🔹 This searches your system for `hive-site.xml`, where Hive’s settings are stored.  

### 📂 Viewing the Hive Configuration File  
Once found, you can open and inspect the configuration file using:  
```bash
cat /etc/hive/conf.dist/hive-site.xml
```
💡 *This helps you check Hive’s settings, including its connection properties!*  

### 🏗️ Hive Metastore Property  
One key property in this file is:  
```xml
javax.jdo.option.ConnectionDriverName
```
- **🔌 Purpose:** Defines the **driver class name** for Hive’s **JDBC metastore**.  
- **🗄️ Hive uses a database as its metastore**, often MySQL or PostgreSQL, to store metadata about tables and partitions.  

---

# 🐬 MySQL Commands for Hive Metastore  

### 🔑 Logging into MySQL as the Hive User  
Run the following command to access the MySQL database Hive uses as its **metastore**:  
```bash
mysql -u hive -p
```
🔹 This prompts you to enter the password for the Hive MySQL user.  

![image](https://github.com/user-attachments/assets/55e1d505-8f18-4cc2-b187-d922038f37a3)  

### 📚 Listing Databases in MySQL  
To view all databases in MySQL, use:  
```sql
SHOW DATABASES;
```
🔹 This reveals the databases stored in MySQL, including Hive’s metastore database.  

![image](https://github.com/user-attachments/assets/2ed7085c-80b7-4be8-8efa-1d1cffc6683b)  

### 📂 Selecting the Hive Metastore Database  
To use the Hive **metastore**, switch to it using:  
```sql
USE metastore;
```
🔹 This ensures you’re working inside Hive’s metadata database.  

![image](https://github.com/user-attachments/assets/dc536da3-2d7d-4d12-a982-b5362177d400)  

### 🗂️ Viewing Tables in the Metastore  
To list all tables stored in the **metastore database**, run:  
```sql
SHOW TABLES;
```
🔹 This shows Hive’s internal tables that store metadata about Hive objects.  

![image](https://github.com/user-attachments/assets/668c70d5-1961-499c-a877-633a889181cd)  

### 🔎 Describing a Table in Metastore  
For detailed table structure, use:  
```sql
DESCRIBE tbls;
```
🔹 This provides **column details** for the specified table.  

![image](https://github.com/user-attachments/assets/761a0274-c05b-4200-a610-4a70c302c77e)  

### 📊 Retrieving Table Names & Types  
To get a list of table names along with their types (managed/external), use:  
```sql
SELECT TBL_NAME, TBL_TYPE FROM TBLS;
```
🔹 This helps you distinguish **internal (managed) and external** Hive tables.  

![image](https://github.com/user-attachments/assets/67040db2-f489-4a26-b08f-8ca73bcfa4b7)  

### 🔎 Expected Output:  
Among the tables listed, you **must see `wh_visits`**, which is likely part of your data stored in Hive!  

---

# 🐝 Hive: Understanding Table Metadata  

### 📜 Listing Tables in Hive  
To list all available tables in Hive, use:  
```sql
SHOW TABLES;
```
🔹 This command retrieves **all table names** present in the database.  

### 🏗️ Where Does This Information Come From?  
- ❌ **Not from HDFS** – The list of tables does **NOT** come directly from the **Hadoop Distributed File System (HDFS)**.  
- ✅ **From Metastore** – The information comes from Hive’s **Metastore**, which stores metadata about tables, partitions, and schema definitions.  

💡 *Think of the Metastore like a database that keeps track of table information, while the actual data resides in HDFS!*  

---

# 🔎 Describing a Hive Table  

### 📂 Viewing Table Structure (`wh_visits`)  
To check the structure and details of a Hive table, use:  
```sql
DESCRIBE wh_visits;
```
🔹 This command shows **column names, data types, and additional properties** of the `wh_visits` table.  

![image](https://github.com/user-attachments/assets/7951b334-c306-4bae-873d-ae0aa2281d06)  

💡 *Example:* If `wh_visits` stores website visits, this command will display details like visitor ID, timestamps, and traffic source categories!  

---

## 🗂️ **Hive Partitions Explained!**  

Partitioning in Hive helps **organize** data efficiently, making queries **faster**! 🚀 Instead of storing everything in a single large table, **Hive partitions** the data into different subdirectories based on specific column values.  

---

### 📌 **Creating a Partitioned Table**  
To create a partitioned table, we use the `partitioned by` clause:  

```sql
CREATE TABLE employees (
    id INT,
    name STRING,
    salary DOUBLE
) PARTITIONED BY (dept STRING);
```
💡 **What this does:**  
- The `dept` column is used to **partition** the table.  
- Data will be **organized into separate folders** based on department values instead of storing everything in one place.  

---

### 📂 **How Partitions are Stored**  
Each partition creates a **subfolder** inside Hive’s warehouse directory:  

📌 **Base directory:** `/apps/hive/warehouse/employees`  
🔹 Subdirectories for each partition value:  
```
/dept=hr/
/dept=support/
/dept=engineering/
/dept=training/
```
💡 **What this means:**  
- Instead of scanning the entire dataset, Hive **only accesses relevant partitions**, improving query speed! ⚡  
- Each department’s data is stored **separately**, making retrieval more efficient.  

---

### 🎯 **Why Use Partitions?**  
✅ **Faster queries** – Hive only searches relevant partitions rather than the entire table.  
✅ **Efficient storage** – Helps organize large datasets effectively.  
✅ **Better scalability** – Works well for huge datasets with repetitive category-based information.  

---

# 📂 Partitioned Tables in Hive  

A **Partitioned Table** is a **special** type of table in Hive that organizes data for efficient retrieval. It differs from a **normal table** because its data is divided into **partitions** based on a specified column.  

### 🏗️ Creating a Partitioned Table  
To create a **managed partitioned table** in Hive:  
```sql
CREATE TABLE employees (
    id INT, 
    name STRING, 
    salary DOUBLE
) 
PARTITIONED BY (dept STRING);
```
✔️ The table is partitioned by the `dept` column, meaning data will be stored separately based on department values.  

![image](https://github.com/user-attachments/assets/d1b53cca-59e0-428d-983a-ae0ffe471bb5)  

### 📤 Loading Data into a Partitioned Table  
When inserting data, you must specify the partition **explicitly**:  
```sql
LOAD DATA LOCAL INPATH 'localpath' INTO TABLE employees PARTITION(dept='hr');
```
✔️ This loads data **only into the `'hr'` partition** of the `employees` table.  

🔹 **Table Types:**  
- **Managed Partition Table** – Hive controls the table’s lifecycle.  
- **External Partition Table** – Data is stored externally, and Hive just manages metadata.  

### 📊 Table Parameters:  
When the partitioned table is **new**, the number of partitions is **0** because **no data has been loaded yet**.  

---

# 🏗️ Bucketed Tables in Hive

![image](https://github.com/user-attachments/assets/ba443e60-649a-469f-93d9-53b21a2c672e)

### 🔢 What is Bucketing?  
Bucketing is **another data-organizing technique** in Hive that **groups similar values** together.  

### 🚀 How Bucketing Works  
✔️ All **same column values** of a **bucketed column** go into the **same bucket**.  
✔️ Bucketing can be used **alone** or **combined with partitioning**.  
✔️ **Buckets are stored as physical files** in Hive.  
✔️ You **explicitly define** the number of buckets during table creation.  

### 📜 Example of Bucketed Table Creation  
```sql
CREATE TABLE employee_data (
    id INT, 
    name STRING, 
    salary DOUBLE
) 
CLUSTERED BY (id) INTO 4 BUCKETS;
```
✔️ The data will be **hashed** into 4 buckets based on the `id` column.  

### 🏎️ Why Use Bucketing?  
✔️ Bucketing can be **more efficient** when used **alone**, rather than with partitioning.  
✔️ **Bucketed Map Joins** are the **fastest joins** in Hive!  

💡 *Example:* Think of bucketing like sorting books into **separate shelves** based on their genre. It speeds up searching when you already know which shelf to look at!  

---

Static Partitioning
Dynamic Partitioning: Hive carries out this. Set certain configuration. Those are critical.

---

Table is not a data. Metadata is the data.
For configuration, we checked hive-site.xml

describe formatted table_name:
Show complete information about table.

Buckets are just the files which runs on HDFS.

What is the purpose of Bucketing, In order to improve the query performance.?
What is the purpose of Partitioning, In order to improve the query performance.?

---

## What is skewed table?

CREATE TABLE Customers (
id int,
username string,
zip int
)
SKEWED BY (zip) ON (57701, 57702)
STORED as DIRECTORIES;

## Sorting Data
Hive has two sorting clauses:
• order by: a complete ordering of the data
• sort by: data output is sorted per reducer

We do order by in SQL

The Map Reduce is not launched when where clause is using partitioned column.
We do order by in RDBMS

There is no sort by in RDBMS
sort by has influence of RDBMS
it always requires reducers to run.

before firing the sort by query, we will write the normal query.
this will be used to sort on the basis of reducer (per reducer), not on the global basis.
We cannot make use of order by then because it is global.

Global ordering: order by in RDBMS
In Hive's Map Reduce: per reducer basis sorting, use sort by and we have to specify reducers

---

## Using Distribute By

insert overwrite table mytable
select gender,age,salary
from salaries
distribute by age;

insert overwrite table mytable
select gender,age,salary
from salaries
distribute by age
sort by age; 

Assume we the no. of reducers to 2, then we fire the first command where we are adding data from salaries into mytable.
When we say distribute by age, the data will inserted in the table only through same reducer which are on the basis of age

Advantages: 2 reducers came into picture here
same age data will be stored in the same reducer
if we apply sort by, we get clustering of data

## Implementation:

talentum@talentum-virtual-machine:~$ cd shared
talentum@talentum-virtual-machine:~/shared$ mkdir hiveDistributeBy
talentum@talentum-virtual-machine:~/shared$ cd hiveDistributeBy/
talentum@talentum-virtual-machine:~/shared/hiveDistributeBy$ nano people.csv
talentum@talentum-virtual-machine:~/shared/hiveDistributeBy$ cat people.csvF,66,41000.0,95103
M,40,76000.0,95102
F,58,95000.0,95103
F,68,60000.0,95105
M,85,14000.0,95102
M,66,84000.0,95102
M,58,95000.0,95107

![image](https://github.com/user-attachments/assets/399b61ef-dd38-4779-9b83-48f2b3e467bf)

talentum@talentum-virtual-machine:~/shared/hiveDistributeBy$ nano people_ddl.hive
talentum@talentum-virtual-machine:~/shared/hiveDistributeBy$ hive -f people_ddl.hive
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/home/talentum/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/home/talentum/hadoop/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in jar:file:/home/talentum/hive/lib/hive-common-2.3.6.jar!/hive-log4j2.properties Async: true
OK
Time taken: 1.891 seconds
OK
Time taken: 0.377 seconds
Loading data to table default.mytable
OK
Time taken: 0.955 seconds

![image](https://github.com/user-attachments/assets/02827e28-1b2f-4a30-bb88-ad78698e6bf2)

talentum@talentum-virtual-machine:~/shared/hiveDistributeBy$ cat people_ddl.hive 
drop table if exists mytable;

create table mytable(gender String, age int, sal double, zip int)
row format delimited
fields terminated by ',';

load data local inpath '/home/talentum/shared/hiveDistributeBy/people.csv' overwrite into table mytable;

---

Now we added more data in people_ddl.hive:

drop table if exists distribute_demo;

create table distribute_demo(gender String, age int, sal double, zip int)
row format delimited
fields terminated by ',';

set mapreduce.job.reduces=2;

insert overwrite table distribute_demo
select gender, age, sal, zip from mytable
distribute by age;

![image](https://github.com/user-attachments/assets/c35320b6-9c2d-4682-84ed-308558411e3e)


---

MapReduce Jobs Launched: 
Stage-Stage-1: Map: 1  Reduce: 2   Cumulative CPU: 2.93 sec   HDFS Read: 12611 HDFS Write: 292 SUCCESS
Total MapReduce CPU Time Spent: 2 seconds 930 msec
OK
Time taken: 24.43 seconds

select * from table;

---

Comment those three lines

and now use sort by

insert overwrite table distribute_demo
select gender, age, sal, zip from mytable
distribute by age sort by age;

What will be the output and how is the output generated. Explain.

Now, we changed:

set mapreduce.job.reduces=3;

What will be the output and how is the output generated. Explain.

---

In RDBMS, we would have used GROUP BY clause.
What if there are millions of records. Then doing group by is efficient?
Why NoSQL never promote group by operation?
They say whichever the data is similar, place them in a group.
Then there is no use of group by.


.hive file
yarn jar should run on hive file
we will have 10 scs
first we will have to use hive and then mapreduce
on inputcounties

Here, the implementation part is over
---

now we are continuing with the notes

## Storing Results to a File

In Big Data World, 99% of times, we are storing the results of the query.

We can store the results of following queries into a file, but where: local or somewhere else?:

INSERT OVERWRITE DIRECTORY 
'/user/train/ca_or_sd/' 
from names
select name, state 
where state = 'CA' 
or state = 'SD';

If we want to store the results into a local file/directory:
This is not used in the production environment

INSERT OVERWRITE LOCAL DIRECTORY
'/tmp/myresults/' 
SELECT * FROM bucketnames 
ORDER BY age;

This feature is not available in RDBMS, but it is available in data Warehouse.

---

## Specifying MapReduce Properties

This is run for hive cli:
SET mapreduce.job.reduces = 12


What if I want to do this setting for my file and not for the entire Hive cli:
hive -f myscript.hive 
-hiveconf mapreduce.job.reduces=12

SELECT * FROM names 
WHERE age = ${age}

The above query has been returned into a file named myscript.hive

hive -f myscript.hive -hivevar age=33

Here, ${age} will be replaced with 33.

In our implementation, we are running:

hive -f people_ddl.hive -hivevar tbl=mytable

since we replaced mytable in hive file to ${tbl}

When giving multiple arguments:

hive -f people_ddl.hive -hivevar tbl=mytable -hivevar tbl2=distribute_demo

since we now replaced tables with ${tbl} and ${tbl2}

---

## Hive Join Strategies

### 🐝 Hive Join Strategies Explained Simply  

Hive provides different join strategies to optimize performance based on data size and structure. Here’s a beginner-friendly breakdown of the key join types, along with an easy-to-understand explanation and examples!  

#### 🔄 Shuffle Join  
**Approach:**  
- Uses **MapReduce** to shuffle join keys across nodes.  
- Joins are performed on the **reduce side**.  

**Pros:**  
✅ Works for **any data size** or layout.  

**Cons:**  
❌ **Slowest** and most resource-intensive join type.  

**Example:**  
Imagine you have two large tables:  
- **Orders** (millions of rows)  
- **Customers** (millions of rows)  

Since both tables are large, Hive distributes the data across multiple nodes, shuffles the matching keys, and performs the join in the reduce phase. This ensures the join works, but it takes more time and resources.  

---

#### 🚀 Map (Broadcast) Join  
**Approach:**  
- **Small tables** are loaded into memory on all nodes.  
- The **mapper** scans through the large table and performs the join.  

**Pros:**  
✅ **Super fast**—only one scan through the largest table.  

**Cons:**  
❌ All but one table **must be small enough** to fit in RAM.  

**Example:**  
Imagine you have:  
- **Orders** (millions of rows)  
- **Country Codes** (only 200 rows)  

Since the **Country Codes** table is small, Hive loads it into memory across all nodes. Then, as the **Orders** table is scanned, it quickly matches country codes without needing a shuffle phase.  

---

#### ⚡ Sort-Merge-Bucket Join  
**Approach:**  
- Uses **pre-sorted and bucketed** tables to perform efficient joins.  
- Mappers take advantage of **co-location of keys** for faster processing.  

**Pros:**  
✅ **Very fast** for tables of any size.  

**Cons:**  
❌ Data **must be sorted and bucketed** ahead of time.  

**Example:**  
Imagine you have:  
- **Orders** (bucketed by customer ID)  
- **Customers** (bucketed by customer ID)  

Since both tables are **bucketed and sorted**, Hive can directly match rows without shuffling, making the join **super efficient**.  

---

### 📝 Key Takeaways  
- **Shuffle Join** → Works for all data sizes but is **slow**.  
- **Map Join** → **Fastest**, but only works when **one table is small**.  
- **Sort-Merge-Bucket Join** → **Efficient**, but requires **pre-sorted and bucketed tables**.  

📌 **Tip:** If possible, **use Map Join** for small tables and **Sort-Merge-Bucket Join** for large, structured data!  

---

### 🔄 Shuffle Joins in Hive  

Shuffle joins are one of the most common join strategies in Hive, especially when dealing with **large datasets**. They work by **shuffling** data across nodes before performing the join operation. Let’s break it down in simple terms!  

![image](https://github.com/user-attachments/assets/ae929f7a-7229-48dd-ae22-e6132229939f)


#### 🛠 How Shuffle Joins Work  
1️⃣ Hive **distributes** the data across multiple nodes.  
2️⃣ The data is **partitioned** based on the join key.  
3️⃣ Matching keys are **shuffled** to the same node.  
4️⃣ The join operation happens in the **reduce phase**.  

#### ✅ Pros of Shuffle Joins  
✔ Works for **any data size**—no restrictions!  
✔ Can handle **large datasets** efficiently.  

#### ❌ Cons of Shuffle Joins  
❌ **Slowest** join type due to heavy data movement.  
❌ Requires **high computational resources**.  

#### 📌 Example  
Imagine you have two large tables:  
- **Customers** (millions of rows)  
- **Orders** (millions of rows)  

Since both tables are **large**, Hive **shuffles** the data across nodes, ensuring that rows with the same customer ID end up on the same node. The join is then performed in the **reduce phase**, making it possible to process massive datasets.  

#### 🖼 Visual Representation  
The image you uploaded illustrates a **shuffle join** using two tables:  
- **Customer Table** (with `id`, `first name`, `last name`)  
- **Orders Table** (with `cid`, `price`, `quantity`)  

The SQL query in the image:  
```sql
SELECT * FROM customer JOIN orders ON customer.id = orders.cid;
```  
This query **joins** the two tables based on the `id` column in **Customer** and the `cid` column in **Orders**, demonstrating how shuffle joins work in SQL.  

### 🚀 Key Takeaways  
- **Shuffle Joins** are **flexible** but **slow** due to data movement.  
- Best used when **both tables are large** and cannot fit in memory.  
- If possible, **opt for Map Joins** when one table is small to improve performance.

## Map (Broadcast) Joins

It will check which table has less data
Distributed cache

## Sort-Merge-Bucket Joins

Requirement of Bucketed Table

---

Types of Optimisers:
RBO: Rule Based Optimisers
CBO: Cost Based Optimisers
All these things will make use of CBO.

---

## Invoking a Hive UDF (User Defined Functions)

There is a process to use UDF

ADD JAR /myapp/lib/myhiveudfs.jar;
CREATE TEMPORARY FUNCTION 
ComputeShipping 
    AS 'hiveudfs.ComputeShipping';
    
FROM orders SELECT
    address, 
    description, 
    ComputeShipping(zip, weight)

Here, ComputeShipping is user defined function

But how to use this function.
We create a java class who gives the implementation of that function.
here, that class is hiveudfs

hive specific class is udf
then give a abstract method - evaluate

compile a class create a jar
ADD JAR /myapp/lib/myhiveudfs.jar;

Then create a temporary function:
CREATE TEMPORARY FUNCTION 
ComputeShipping 
    AS 'hiveudfs.ComputeShipping';

---

Lab:

create a project with package hiveudfs

project: HiveUDF

filesystem > usr > hive > lib > select all jars but do not select the two folders > OK > OK
create jar > hiveudf.jar
put this file in the labshome area/path

---

## Computing ngrams in Hive

ngrams:
Collec

select ngrams(sentences(val),2,100) 
from mytable;
select context_ngrams(sentences(val),
array("error","code",null),
100)
from mytable;

Top 100 words appearing after error code

---

## Lesson Review
1. A Hive table consists of a schema stored in the Hive ___________ and data stored 
in _______________. metastore, hdfs

3. True or False: The Hive metastore requires an underlying SQL database. True

5. What happens to the underlying data of a Hive-managed table when the table is 
dropped? Data is deleted

7. True or False: A Hive external table must define a LOCATION. Not mandatory

9. List three different ways data can be loaded into a Hive table.
load data
local inpath
insert record

10. When would you use a skewed table?

12. What will the folder structure in HDFS look like for the movies table?
create table movies (title string, rating string, length double) partitioned by 
(genre string);
/user/hive/warehouse/movies/

14. Explain the output of the following query:
select * from movies order by title;
global ordering

16. What does the following Hive query compute? 
from mytable select 
explode(ngrams(sentences(val),3,100)) as myresult;
top 100 trigrams

18. What does the following Hive query compute? 
from mytable select explode(
context_ngrams(sentences(val),
array("I","liked",null),10)) as myresult;

---

Avro: Row oriented binary file format

Apache Avro[79] is a language-neutral data serialization system. The project was created by Doug Cutting (the creator of Hadoop) to address the major downside of Hadoop Writables: lack of language portability. Having a data format that can be processed by many languages (currently C, C++, C#, Java, JavaScript, Perl, PHP, Python, and Ruby) makes it easier to share datasets with a wider audience than one tied to a single language. It is also more future-proof, allowing data to potentially outlive the language used to read and write it.

But why a new data serialization system? Avro has a set of features that, taken together, differentiate it from other systems such as Apache Thrift or Google’s Protocol Buffers.[80] Like in these systems and others, Avro data is described using a language-independent schema. However, unlike in some other systems, code generation is optional in Avro, which means you can read and write data that conforms to a given schema even if your code has not seen that particular schema before. To achieve this, Avro assumes that the schema is always present—at both read and write time—which makes for a very compact encoding, since encoded values do not need to be tagged with a field identifier.

Avro schemas are usually written in JSON, and data is usually encoded using a binary format, but there are other options, too. There is a higher-level language called Avro IDL for writing schemas in a C-like language that is more familiar to developers.

---

## Advanced Hive Programming

## Topics to be Covered
• Performing a Multi-Table/File Insert • Understanding Views
• Defining Views
• Using Views
• The OVER Clause
• Using Windows
• Hive Analytics Functions
• Lab: Advanced Hive Programming
• Hive File Formats
• Hive SerDe

## Performing a Multi-Table/File Insert 

![image](https://github.com/user-attachments/assets/a805fc63-f8b5-498c-aedf-e02d38a6f8c2)

insert overwrite directory '2014_visitors' select * from wh_visits 
where visit_year='2014' 
insert overwrite directory 'ca_congress' select * from congress 
where state='CA' ;
No semicolon
from visitors
INSERT OVERWRITE TABLE gender_sum
SELECT visitors.gender, count_distinct(visitors.userid)
GROUP BY visitors.gender
INSERT OVERWRITE DIRECTORY '/user/tmp/age_sum'
SELECT visitors.age, count_distinct(visitors.userid)
GROUP BY visitors.age;

📌 **Understanding Views in Hive** 🐝

![image](https://github.com/user-attachments/assets/fa1bac13-de9e-4b10-bb45-f5854ee54b2d)


In **Hive**, views play a crucial role in organizing and accessing data efficiently. Let's break it down step by step in simple terms! 

### 🔍 **What Are Views?**
A **View** in Hive is like a **virtual table**—it is **not physically stored** but is created based on a query. Think of it like a saved search that generates results dynamically whenever you access it.

### 🗄️ **Hive Tables vs. Hive Views**
- **Hive Tables** 📂: These map directly to **folders in HDFS (Hadoop Distributed File System)**, meaning they store actual data.
- **Hive Views** 👀: These are **query-generated** results and **do not store any data** physically.

### 📌 **How Views Work**
Imagine a massive dataset containing stock prices from different companies 📊. If you frequently need to analyze just the tech stocks, instead of creating a new table, you can create a **view** that always retrieves tech stocks using a predefined query.

Example:
```sql
CREATE VIEW tech_stocks AS 
SELECT * FROM stock_data WHERE sector = 'Technology';
```
Now, whenever you query `tech_stocks`, you get the latest filtered data without needing to store it separately.

### 📷 **Visual Representation**
Your image illustrates this concept beautifully:
- **Tables (Table_1, Table_2, Table_3)** in Hive map to **HDFS folders** ✅.
- **Views (View_1, View_2)** exist in the **Hive Metastore** but don’t have direct storage in HDFS ⚡.
- Views are **simply stored queries**, making data retrieval efficient without unnecessary storage use.

### 🎯 **Key Benefits of Using Views**
✅ No extra storage consumption 🚀  
✅ Faster data access for common queries 📊  
✅ Simplifies data organization 💡  


## Defining Views
CREATE VIEW 2010_visitors AS 
SELECT fname, lname, 
time_of_arrival, info_comment
FROM wh_visits 
WHERE
cast(substring(time_of_arrival,6,4) 
AS int) >= 2010 
AND 
cast(substring(time_of_arrival,6,4) 
AS int) < 2011;

## Using Views
You use a view just like a 
table:
from 2010_visitors 
select * 
where info_comment like "%CONGRESS%" 
order by lname;

📌 **Understanding the OVER Clause in SQL** ⚡

![image](https://github.com/user-attachments/assets/96032962-fcf6-4e5d-948a-04a7299850b2)


The **OVER** clause in SQL is a powerful tool that allows you to perform calculations across a specific set of rows, without needing to group your data. Let’s break it down in simple terms! 😊

### 🔍 **What Does the OVER Clause Do?**
- It helps apply **window functions**, meaning you can compute values **without collapsing rows** like `GROUP BY` does.
- It lets you define a **partition**, similar to creating mini-groups inside your data.

### 🔄 **Comparing GROUP BY vs. OVER Clause**
Imagine you have a table called **`orders`** containing customer IDs (`cid`), product prices, and quantities. You want to find the **highest price per customer**.

#### ✅ Using `GROUP BY` (Collapses Rows)
```sql
SELECT cid, max(price) FROM orders GROUP BY cid;
```
💡 **Result:** You get one row per customer (`cid`) with the maximum price, but **other details are lost**.

#### 🔥 Using `OVER` with `PARTITION BY` (Keeps Rows Intact)
```sql
SELECT cid, price, max(price) OVER (PARTITION BY cid) FROM orders;
```
💡 **Result:** You get **all rows**, but with an additional column showing the maximum price **without removing details!**

### 📷 **Visual Representation** 
Your image illustrates this concept beautifully:
- **GROUP BY** shrinks results, showing only the `cid` and maximum price.
- **OVER (PARTITION BY cid)** keeps all data intact while still displaying the max price.

### 🎯 **Key Benefits of Using the OVER Clause**
✅ Keeps all details while applying calculations 🚀  
✅ Helps in advanced analytics, like running totals and ranking 📊  
✅ Works great with window functions (e.g., `ROW_NUMBER()`, `RANK()`, `SUM() OVER()`)  

---

📌 **Understanding Window Functions in SQL** 🏢  

![image](https://github.com/user-attachments/assets/37ca782c-39bb-4e1b-8e49-c13ca31bf932)


Window functions in SQL allow us to perform **calculations across a specific set of rows** in a dataset, without collapsing the data like `GROUP BY`. Let’s break it down in simple terms! 😊  

---

### 🔍 **What Are Window Functions?**  
A **window function** operates over a **specific range of rows**, known as the **window**, instead of working on the entire dataset. It **does not remove duplicates or group data**, unlike `GROUP BY`.  

Think of it as applying calculations **inside each mini-group**, rather than across the entire table.  

---

### 🖥️ **How Window Functions Work**  
Imagine you have a dataset of **orders** containing customer IDs (`cid`), product prices, and quantities. You want to calculate the **sum of prices for each customer, considering the last two prices** before the current row.  

📜 **SQL Query:**
```sql
SELECT cid, 
       SUM(price) OVER (PARTITION BY cid ORDER BY price ROWS BETWEEN 2 PRECEDING AND CURRENT ROW)
FROM orders;
```
💡 **Breaking It Down:**  
✅ `PARTITION BY cid` → Divides data into groups based on `cid` (each customer)  
✅ `ORDER BY price` → Sorts the data within each partition  
✅ `ROWS BETWEEN 2 PRECEDING AND CURRENT ROW` → Includes the **current row and the two rows before it** for calculation  

---

### 📷 **Visual Representation**  
Your image illustrates this concept clearly:  
- The **orders table** contains `cid`, `price`, and `quantity`.  
- The **result set** shows how the sum of prices is computed by **considering the current row and the two preceding rows** in each partition.  

---

### 🎯 **Key Benefits of Using Window Functions**
✅ Retains original rows while applying calculations 🚀  
✅ Useful for **running totals**, **moving averages**, and **rankings** 📊  
✅ Provides more flexibility than `GROUP BY`  

---

## Using Windows – cont.
SELECT cid, sum(price) OVER 
(PARTITION BY cid ORDER BY price ROWS 
BETWEEN 2 PRECEDING AND 3 FOLLOWING) 
FROM orders;
SELECT cid, sum(price) OVER 
(PARTITION BY cid ORDER BY price ROWS 
BETWEEN UNBOUNDED PRECEDING AND 
CURRENT ROW) FROM orders;

---

📌 **Hive Analytical Functions** 📊  

![image](https://github.com/user-attachments/assets/3345e13c-5789-4892-9ed6-efb3e8bca1b0)

Hive provides powerful **analytical functions** that help in complex data processing, allowing you to perform calculations across sets of rows efficiently. Let's break them down in simple terms! 😊  

---

### 🔍 **What Are Analytical Functions in Hive?**  
Analytical functions in Hive **process data across multiple rows** and return a value for each row without grouping data. Unlike regular aggregation functions (`SUM()`, `AVG()`), analytical functions **retain individual row data** while applying calculations within a defined window.  

Think of it as applying calculations **without shrinking your dataset**, which is great for **ranking, running totals, and moving averages**.  

---

### 🛠️ **Common Analytical Functions in Hive**  

✅ **RANK()** 🏆 → Assigns a rank to rows based on a specified order.  
✅ **DENSE_RANK()** 🥇 → Similar to `RANK()`, but without gaps in ranking numbers.  
✅ **ROW_NUMBER()** 🔢 → Assigns a unique row number starting from 1.  
✅ **NTILE(N)** 🔄 → Divides rows into **N groups** evenly.  
✅ **LEAD() & LAG()** 🔄 → Fetches the **next or previous row's value**, useful for comparisons.  

---

### 🖥️ **Example Usage**  

Imagine we have a dataset of **employees** with their names and salaries:  

📜 **SQL Query to Rank Employees by Salary**  
```sql
SELECT name, salary, RANK() OVER (ORDER BY salary DESC) AS rank 
FROM employees;
```
💡 **Breaking It Down:**  
✅ `ORDER BY salary DESC` → Orders employees by highest salary first  
✅ `RANK() OVER (...)` → Assigns ranking based on salary  

📊 **Example Output:**  
| Name  | Salary | Rank |
|-------|--------|------|
| Alice | 80K    | 1    |
| Bob   | 75K    | 2    |
| Carol | 75K    | 2    |
| Dave  | 70K    | 4    |

🔍 **Notice**: Carol and Bob **have the same salary**, so they share Rank 2!  

---

### 📷 **Visual Representation**  
Your image illustrates this concept beautifully, showing different analytical functions and how they work in Hive queries.  

---

### 🎯 **Key Benefits of Using Hive Analytical Functions**  
✅ Perform **ranking, running totals, and comparisons** easily 🚀  
✅ Avoid unnecessary grouping while applying calculations 🔄  
✅ Improve **data analysis for large datasets** 📊  



































