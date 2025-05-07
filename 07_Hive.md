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

Here's your refined version of "Hive's Alignment with SQL" with structured explanations and simple language! 🚀📚  

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

Here’s your refined, beginner-friendly version of the notes with explanations, structured details, and emojis for better clarity! 🚀📚  

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

Here’s your refined, beginner-friendly version of the notes with explanations, emojis, and structured details for better understanding! 🚀📚  

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
