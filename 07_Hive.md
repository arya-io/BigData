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

# 🧱 Static vs Dynamic Partitioning in Hive

## 📦 Static Partitioning

* In **Static Partitioning**, you manually specify the partition column value when loading data.
* Example:

  ```sql
  LOAD DATA INPATH '/data/customers.csv' 
  INTO TABLE customers 
  PARTITION (country='India');
  ```
* ✅ Simple, but not scalable when you have many partitions.

## 🔄 Dynamic Partitioning

* **Dynamic Partitioning** is handled automatically by **Hive**.
* Hive figures out the partition values **during query execution**.
* 🔧 We configure it using the `hive-site.xml` file.

  **Important configurations**:

  ```sql
  SET hive.exec.dynamic.partition = true;
  SET hive.exec.dynamic.partition.mode = nonstrict;
  ```

🧠 **Why do we use Partitioning?**
👉 To **speed up query performance** by scanning only relevant data.

---

# 🧾 Metadata ≠ Data

> “**Table is not the data. Metadata is the data.**”

What does this mean?
Hive tables store **metadata** (like column names, data types, location, etc.) in the metastore.
But actual **data lives in HDFS**.

To view full metadata of a table:

```sql
DESCRIBE FORMATTED table_name;
```

---

# 🪣 Bucketing in Hive

* Buckets are just **files in HDFS**. Think of them as smaller partitions inside a table.
* Used to **divide data into more manageable chunks** based on a **hash function**.
* 🎯 Purpose: **Improve query performance**, especially when JOINing large tables.

💡 You can use bucketing when:

* You have a **large dataset**.
* You want **optimized JOINs** and **sampling**.

---

# ❓ What is a Skewed Table?

Some values in a column appear **much more frequently** than others. This creates an imbalance in data distribution.

### 🧪 Example:

```sql
CREATE TABLE Customers (
  id INT,
  username STRING,
  zip INT
)
SKEWED BY (zip) ON (57701, 57702)
STORED AS DIRECTORIES;
```

Here, `zip` values `57701` and `57702` are skewed (occur very frequently), so Hive stores them **separately** to handle load better.

---

# 🌀 Sorting in Hive

Hive provides two types of sorting:

## 📚 `ORDER BY`

* Sorts **all data globally**.
* Only one reducer is used → may be **slow for large datasets**.
* Just like `ORDER BY` in **SQL/RDBMS**.

## 🔀 `SORT BY`

* Sorts data **within each reducer** (not global).
* More efficient than `ORDER BY` for large datasets.
* ❗Requires you to define the number of reducers.

  Example:

  ```sql
  SET mapreduce.job.reduces = 4;
  SELECT * FROM table_name SORT BY column_name;
  ```

🧠 Summary:

| Feature     | ORDER BY       | SORT BY                    |
| ----------- | -------------- | -------------------------- |
| Scope       | Global sort    | Per reducer (partial sort) |
| Reducers    | Single reducer | Multiple reducers          |
| RDBMS Match | Yes            | No                         |

---

# 💡 Bonus Insight: Query Optimization

* When using **partitioned columns in WHERE clause**, Hive doesn’t launch MapReduce jobs.
  Example:

  ```sql
  SELECT * FROM sales WHERE country = 'India';
  ```

  👉 This avoids full table scan = faster!

---

# 🔁 Using `DISTRIBUTE BY` in Hive

## 🧩 What is `DISTRIBUTE BY`?

`DISTRIBUTE BY` decides **how the data is split and sent to reducers** in a MapReduce job.
It ensures that **rows with the same value** of a specified column go to the **same reducer**.

---

### 🛠️ Syntax Example:

```sql
INSERT OVERWRITE TABLE mytable
SELECT gender, age, salary
FROM salaries
DISTRIBUTE BY age;
```

👉 Here, all records with the **same `age`** will go to the **same reducer**.

---

### 🧠 Real-World Analogy:

Imagine sorting letters by ZIP code in a post office.
Each ZIP code bucket (age in our case) goes to a specific delivery person (reducer).

---

### 🔀 With Sorting:

```sql
INSERT OVERWRITE TABLE mytable
SELECT gender, age, salary
FROM salaries
DISTRIBUTE BY age
SORT BY age;
```

* `DISTRIBUTE BY` → groups the data by age (to reducers).
* `SORT BY` → sorts the data **within each reducer**.
* ✅ This helps in **clustering** similar values together.

---

## 🛠️ Reducers and `DISTRIBUTE BY`

If you set:

```sql
SET mapreduce.job.reduces = 2;
```

👉 Hive uses **2 reducers**, and the data is distributed among them **based on age**.

✨ Benefits:

* More parallelism → **better performance**.
* **Same-age data** stays together.
* Combined with `SORT BY` → helps in **data clustering**.

---

# 🧪 Practical Implementation

### 📁 Step-by-Step in Terminal:

```bash
cd ~/shared
mkdir hiveDistributeBy
cd hiveDistributeBy/
nano people.csv
```

### 🧾 Sample `people.csv` File:

```
F,66,41000.0,95103
M,40,76000.0,95102
F,58,95000.0,95103
F,68,60000.0,95105
M,85,14000.0,95102
M,66,84000.0,95102
M,58,95000.0,95107
```

![people.csv image](https://github.com/user-attachments/assets/399b61ef-dd38-4779-9b83-48f2b3e467bf)

---

### 🧾 people\_ddl.hive (Table Creation & Load)

```sql
DROP TABLE IF EXISTS mytable;

CREATE TABLE mytable (
  gender STRING,
  age INT,
  sal DOUBLE,
  zip INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';

LOAD DATA LOCAL INPATH '/home/talentum/shared/hiveDistributeBy/people.csv'
OVERWRITE INTO TABLE mytable;
```

📦 Execution:

```bash
hive -f people_ddl.hive
```

✅ Output Logs:

```
SLF4J: Multiple bindings found...
Logging initialized...
Loading data to table default.mytable
OK
```

![hive log image](https://github.com/user-attachments/assets/02827e28-1b2f-4a30-bb88-ad78698e6bf2)

---

# 📤 Now: Distribute Data into Another Table

### 📄 Add this to `people_ddl.hive`:

```sql
DROP TABLE IF EXISTS distribute_demo;

CREATE TABLE distribute_demo (
  gender STRING,
  age INT,
  sal DOUBLE,
  zip INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ',';

SET mapreduce.job.reduces = 2;

INSERT OVERWRITE TABLE distribute_demo
SELECT gender, age, sal, zip
FROM mytable
DISTRIBUTE BY age;
```

📊 This ensures that:

* Data is split between **2 reducers**.
* Rows with same **age** go to **same reducer**.

![distribute\_demo result](https://github.com/user-attachments/assets/c35320b6-9c2d-4682-84ed-308558411e3e)

---

✅ **Quick Recap**:

| Clause        | Purpose                             |
| ------------- | ----------------------------------- |
| DISTRIBUTE BY | Groups data sent to each reducer    |
| SORT BY       | Sorts data within each reducer      |
| ORDER BY      | Global sort (only one reducer used) |

---

# ⚙️ MapReduce Job Info in Hive

When we run a Hive query, it internally triggers **MapReduce jobs**.
Example output:

```
MapReduce Jobs Launched: 
Stage-Stage-1: Map: 1  Reduce: 2   Cumulative CPU: 2.93 sec   HDFS Read: 12611 HDFS Write: 292 SUCCESS
Total MapReduce CPU Time Spent: 2 seconds 930 msec
Time taken: 24.43 seconds
```

👉 This tells us:

* **How many Mappers and Reducers** were used.
* **CPU time** and **I/O operations**.
* Whether the job was **successful** or not.

---

# 🧪 Sorting with `DISTRIBUTE BY` + `SORT BY`

```sql
INSERT OVERWRITE TABLE distribute_demo
SELECT gender, age, sal, zip 
FROM mytable
DISTRIBUTE BY age 
SORT BY age;
```

🧠 **Explanation of Output (with 2 reducers)**:

* Data is **distributed by `age`** → all rows with same age go to the same reducer.
* Within each reducer, data is **sorted by `age`** → resulting in **clustered, sorted data** *locally* per reducer.
* Final output = files from each reducer with sorted chunks of data.

---

# 🔁 Now With 3 Reducers

```sql
SET mapreduce.job.reduces = 3;
```

📌 What happens?

* Data is split among **3 reducers** based on `age`.
* `DISTRIBUTE BY age` ensures:

  * Same-age records → same reducer.
* `SORT BY age` ensures:

  * Within each reducer → data is sorted by age.

💡 But since reducers work **independently**, global ordering is **not guaranteed** (use `ORDER BY` if you want that, but it uses only one reducer).

---

# 🧮 RDBMS vs Hive on Grouping

## 🏛️ In RDBMS (like MySQL, PostgreSQL):

```sql
SELECT gender, COUNT(*) 
FROM mytable 
GROUP BY gender;
```

✅ Works well for small to medium datasets.

---

## 🏢 But in Big Data? (Millions of Records)

* `GROUP BY` becomes **expensive** due to data shuffling.
* In distributed systems (Hive/NoSQL), grouping = **data movement** = performance hit.

---

## ❌ Why NoSQL Avoids GROUP BY

* NoSQL promotes **pre-grouping**:
  “Store similar data together” → design schema in a way that reduces need for grouping later.

🚫 This avoids expensive **grouping operations** on huge data at query time.

---

# 📦 Running Hive Scripts with YARN

You can execute a `.hive` file like this:

```bash
hive -f yourfile.hive
```

Hive internally launches **MapReduce jobs via YARN**.
So you may see lines like:

```bash
yarn jar ...
```

💡 Example:

* Input file: `inputcounties`
* You may need to run **multiple scripts (10 scs)** using Hive, followed by MapReduce.

---

# 📁 Storing Query Results to Files

## 💼 99% of the time in Big Data, we **store results** of a query, not just display them.

### 💾 HDFS Output (Production Use)

```sql
INSERT OVERWRITE DIRECTORY '/user/train/ca_or_sd/'
FROM names
SELECT name, state 
WHERE state = 'CA' OR state = 'SD';
```

✅ Output is stored in **HDFS**, ideal for **production**.

---

### 🖥️ Local Output (Not for Production)

```sql
INSERT OVERWRITE LOCAL DIRECTORY '/tmp/myresults/'
SELECT * FROM bucketnames
ORDER BY age;
```

📌 Useful for **testing** or **personal exploration**, but:

* ❌ Not used in production environments.

---

### 🧠 Bonus Insight:

🛢️ This capability of storing results directly into directories is **not available in traditional RDBMS**,
but it's a **powerful feature** in Data Warehouses like Hive.

---

# 🛠️ Specifying MapReduce Properties in Hive

In Hive, you can customize how MapReduce jobs behave using properties.

## 🌐 Setting for Hive CLI Session

If you're working directly in the Hive CLI:

```sql
SET mapreduce.job.reduces = 12;
```

🔧 This sets the number of reducers for **that session** only.

---

## 📄 Setting via Hive Script File

If you want to set properties for a specific `.hive` script file:

```bash
hive -f myscript.hive -hiveconf mapreduce.job.reduces=12
```

💡 This sets the reducer count only **for that file's execution**—not for the entire CLI.

---

# 💡 Using Variables in Hive Scripts

Hive supports **variable substitution** using `${}` syntax. This helps write **dynamic scripts**!

### 🧾 Example Script (myscript.hive):

```sql
SELECT * FROM names WHERE age = ${age};
```

You can run this script and pass the variable `age` as:

```bash
hive -f myscript.hive -hivevar age=33
```

✅ Output: Hive replaces `${age}` with `33` → runs the actual query.

---

### 🧪 Real-World Use Case

Let’s say you want to reuse a script for different table names:

#### Inside your `people_ddl.hive` file:

```sql
DROP TABLE IF EXISTS ${tbl};
CREATE TABLE ${tbl}(gender STRING, age INT, sal DOUBLE, zip INT) 
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY ',';
```

### ▶️ Run the script:

```bash
hive -f people_ddl.hive -hivevar tbl=mytable
```

📌 Hive will replace `${tbl}` with `mytable`.

---

### 🔗 Using Multiple Variables

You can pass **more than one variable**:

```bash
hive -f people_ddl.hive -hivevar tbl=mytable -hivevar tbl2=distribute_demo
```

And your `.hive` file can contain both:

```sql
INSERT INTO ${tbl2}
SELECT * FROM ${tbl};
```

🧠 This makes your Hive scripts **modular**, **flexible**, and easier to maintain!

---

✅ **Summary Cheat Sheet**:

| Task                        | Command Example                                            |
| --------------------------- | ---------------------------------------------------------- |
| Set reducer count for CLI   | `SET mapreduce.job.reduces = 12;`                          |
| Set reducer count in script | `hive -f myscript.hive -hiveconf mapreduce.job.reduces=12` |
| Pass variable to script     | `hive -f myscript.hive -hivevar age=33`                    |
| Pass multiple variables     | `-hivevar tbl=table1 -hivevar tbl2=table2`                 |

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

---

# 🔄 Map (Broadcast) Joins

### 🧩 What happens in a **Map Join**?

When Hive executes a **Map Join**, it checks:

* 🧮 **Which table is smaller in size?**

If a table is **small enough to fit in memory**, Hive **broadcasts it to all mappers** using a mechanism called the **Distributed Cache**.

### ✅ Why is this useful?

👉 Avoids reducer stage (no shuffle phase), so it is **much faster**!

📦 Example:

> You’re joining a big `orders` table with a small `cities` table. Hive will send the `cities` table to all mappers and complete the join **in the map phase itself**.

---

# 🔗 Sort-Merge-Bucket Joins

### 🪣 What are these?

This type of join is used **only when**:

* ✅ Tables are **bucketed**
* ✅ Tables are **sorted** on the join key
* ✅ Number of buckets should match

🧠 Used for **very large datasets** where Map Join isn't suitable.

📌 **Benefit**: Optimized join performance with better parallelism and minimal shuffle.

---

# 🧠 Types of Hive Optimizers

Hive uses two types of optimizers for improving query performance:

| Optimizer | Full Form            | How it works                                                                                              |
| --------- | -------------------- | --------------------------------------------------------------------------------------------------------- |
| 🧱 RBO    | Rule-Based Optimizer | Uses predefined rules (e.g., push filters down first)                                                     |
| 🧮 CBO    | Cost-Based Optimizer | Evaluates multiple plans and chooses the most efficient one based on **cost estimates** like time, memory |

✅ Hive uses **CBO** in modern versions for advanced query planning.

---

# 🔧 Using Hive UDFs (User-Defined Functions)

Sometimes, Hive's built-in functions aren’t enough. You can create your own logic using **Java**, and plug it into Hive using UDFs!

## 📦 Step-by-Step: How to Use a Hive UDF

1. **Create a Java Class**
   It should:

   * Extend Hive’s `UDF` class
   * Implement an `evaluate()` method

```java
public class ComputeShipping extends UDF {
   public double evaluate(int zip, double weight) {
       // your logic here
   }
}
```

2. **Compile and Package into a JAR**

```bash
jar -cvf myhiveudfs.jar hiveudfs/ComputeShipping.class
```

3. **Register the JAR in Hive**

```sql
ADD JAR /myapp/lib/myhiveudfs.jar;
```

4. **Create a Temporary Function**

```sql
CREATE TEMPORARY FUNCTION ComputeShipping AS 'hiveudfs.ComputeShipping';
```

5. **Use the Function in Queries**

```sql
FROM orders 
SELECT 
    address, 
    description, 
    ComputeShipping(zip, weight);
```

🧠 Note: The function works **only during the current Hive session** (temporary).

---

✅ **Why Use UDFs?**

* To add **custom business logic** that Hive’s built-in functions can’t do.
* Great for **data transformation**, custom validation, etc.

---

# 🧪 Hive UDF Lab Setup: Step-by-Step Guide

## 🏗️ Step 1: Create the Java Project

### 📂 Project Name: `HiveUDF`

### 📦 Package Name: `hiveudfs`

This package will contain your custom Java class for the UDF.

---

## 📄 Step 2: Create the UDF Java Class

Example class:

```java
package hiveudfs;

import org.apache.hadoop.hive.ql.exec.UDF;

public class ComputeShipping extends UDF {
    public double evaluate(int zip, double weight) {
        // Sample logic: shipping cost = weight * rate based on zip
        if (zip == 95103) {
            return weight * 2.0;
        } else {
            return weight * 1.5;
        }
    }
}
```

---

## ⚙️ Step 3: Add Hive JARs to Classpath

Go to your Java project’s **Build Path** settings:

1. Right-click on the project → `Build Path` → `Configure Build Path`
2. Go to the **Libraries** tab → `Add External JARs`
3. Navigate to:
   **`/usr/hive/lib/`**
4. **Select all the `.jar` files** in this directory ✅
   **DO NOT select the two folders** ❌
5. Click `OK` → `Apply and Close`

📦 These Hive JARs provide the classes needed to compile your UDF.

---

## 🧪 Step 4: Create the JAR File

Now, package your class into a `.jar` file:

1. Right-click on the project → `Export`
2. Select: `Java` → `JAR file` → `Next`
3. Select your `hiveudfs` package
4. Choose the destination file path as:

```
/home/talentum/labshome/hiveudf.jar
```

5. Click `Finish`

🎉 You’ve successfully created your UDF JAR!

---

✅ Now you can use this JAR in Hive like this:

```sql
ADD JAR /home/talentum/labshome/hiveudf.jar;

CREATE TEMPORARY FUNCTION ComputeShipping AS 'hiveudfs.ComputeShipping';

SELECT name, weight, ComputeShipping(zip, weight) FROM orders;
```

---

# 📚 **Ngrams in Hive**: Text Analysis Made Easy 🗣️

## 🔍 What Are Ngrams?

👉 **N-grams** are simply **sequences of N words** from a given text.

* A **bigram** is 2 consecutive words (N=2)
* A **trigram** is 3 consecutive words (N=3), and so on.

### 🛠️ Use Case:

Used in **text analytics**, **search engines**, **autocorrect**, **spam filters**, etc.

---

## 🧪 Hive Functions to Compute Ngrams

### ➕ Example 1: Extracting Top 100 Bigrams (2-word sequences)

```sql
SELECT ngrams(sentences(val), 2, 100) 
FROM mytable;
```

📌 **Explanation**:

* `sentences(val)` splits the text in the `val` column into individual sentences.
* `ngrams(..., 2, 100)` extracts **bigrams** (2-word phrases).
* **Top 100** results are returned.

---

### ➕ Example 2: Contextual Ngrams 📌

```sql
SELECT context_ngrams(sentences(val), 
ARRAY("error", "code", NULL), 100) 
FROM mytable;
```

📌 **Explanation**:

* This finds the **top 100 words that appear after the phrase "error code"** in the text.
* The `NULL` indicates a placeholder for the word you want to find after the given context.

---

# ✅ **Lesson Review**: Quick Check 🧠

1️⃣ **A Hive table consists of a schema stored in the Hive `metastore` and data stored in `HDFS`.**

3️⃣ **True or False:**
The Hive **metastore** requires an underlying SQL database?
✅ **True**

5️⃣ **What happens to the underlying data of a Hive-managed table when the table is dropped?**
🗑️ The **data is deleted**.

7️⃣ **True or False:**
A Hive external table must define a LOCATION?
❌ **False** – It’s not mandatory, but usually provided.

9️⃣ **List 3 Ways to Load Data into a Hive Table:**

* `LOAD DATA`
* `LOCAL INPATH`
* `INSERT RECORD`

🔟 **When would you use a skewed table?**
👉 When certain values (like specific ZIP codes) occur **very frequently**, skewing the data distribution and affecting performance.
Helps improve performance by treating those values differently.

---

## 📁 HDFS Folder Structure Example

📌 **Table:**

```sql
CREATE TABLE movies (
  title STRING,
  rating STRING,
  length DOUBLE
) PARTITIONED BY (genre STRING);
```

📁 **HDFS Location:**

```
/user/hive/warehouse/movies/
```

---

## 🔠 Ordering in Hive

```sql
SELECT * FROM movies ORDER BY title;
```

🧾 **Output Explanation**:
This gives a **global ordering** of all records by `title`. It uses **1 reducer** to maintain a consistent order.

---

## 🧠 Text Analytics Queries Explained

### ▶️ **Trigram Extraction (3-word sequences)**

```sql
FROM mytable
SELECT EXPLODE(ngrams(sentences(val), 3, 100)) AS myresult;
```

📌 **Explanation**: Extracts **top 100 trigrams** from the text in `val`.

---

### ▶️ **Contextual Trigrams**

```sql
FROM mytable 
SELECT EXPLODE(
  context_ngrams(sentences(val),
  ARRAY("I", "liked", NULL), 10)) AS myresult;
```

📌 **Explanation**:
Finds **top 10 words** that most frequently appear **after "I liked"** in the text.

---
Here’s your next set of **Big Data (Hive + Avro + Advanced Hive Programming)** notes, refined for clarity, engagement, and revision ease 📘🚀:

---

# 🧊 **Avro: Row-Oriented Binary File Format**

### 🔧 What is Avro?

Avro is a **language-neutral** data serialization system developed by **Doug Cutting** (yes, the creator of Hadoop! 🐘).

### 🎯 Why Avro?

* Solves Hadoop’s **language portability issue** with Writables
* Works with multiple languages:
  `Java, Python, C, C++, C#, PHP, JavaScript, Perl, Ruby`

### ⚙️ Key Features of Avro

✅ **Schema-based** (written in JSON)
✅ **Binary format** for compact, fast I/O
✅ **Code generation is optional**
✅ **Schema must be present at both read and write time**
✅ **Future-proof** — data can outlive the application
✅ Also supports a C-like syntax via **Avro IDL**

📌 **Comparison**:

| Feature         | Avro                        | Thrift/Protobuf          |
| --------------- | --------------------------- | ------------------------ |
| Schema format   | JSON                        | Custom or IDL            |
| Code generation | Optional                    | Required                 |
| Field tags      | Not required                | Required                 |
| Use case        | Big Data, Hadoop ecosystems | General purpose RPC/data |

---

# 👩‍💻 **Advanced Hive Programming**

## 🎯 Topics To Be Covered:

* ✅ Multi-Table/File Insert
* ✅ Views: Creating & Using
* ✅ `OVER` Clause
* ✅ Window Functions
* ✅ Hive Analytics Functions
* ✅ Hive File Formats & SerDe
* ✅ 🧪 Lab Practice

---

## 📥 Performing a Multi-Table/File Insert

Hive allows **writing to multiple outputs** (tables/directories) from a **single query**! 🚀

### 💡 Syntax Example:

```sql
FROM wh_visits
INSERT OVERWRITE DIRECTORY '2014_visitors'
SELECT * 
WHERE visit_year = '2014'

INSERT OVERWRITE DIRECTORY 'ca_congress'
SELECT * 
FROM congress 
WHERE state = 'CA';
```

⚠️ **Note**: No semicolon `;` until all `INSERT` statements are finished.

---

### ➕ Another Example:

```sql
FROM visitors
INSERT OVERWRITE TABLE gender_sum
SELECT gender, COUNT(DISTINCT userid)
GROUP BY gender

INSERT OVERWRITE DIRECTORY '/user/tmp/age_sum'
SELECT age, COUNT(DISTINCT userid)
GROUP BY age;
```

📌 **Why use this?**

* Faster than writing separate queries
* Efficient for reporting and exporting
* Reduces processing time by **reusing the same data scan**

---

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

# 🔍 **Window Functions in Hive**

### 📌 What is a Window Function?

A **Window Function** performs calculations **across a set of rows (a window)** related to the current row.

🔄 Unlike `GROUP BY`:

* It **doesn't collapse rows**
* Original rows are **retained**
* Ideal for **ranking**, **running totals**, **moving averages**, etc.

---

## 🛠️ **How It Works**

### 👇 Query Example:

```sql
SELECT cid, 
       SUM(price) OVER (
           PARTITION BY cid 
           ORDER BY price 
           ROWS BETWEEN 2 PRECEDING AND CURRENT ROW
       ) AS running_sum
FROM orders;
```

### 🔍 Breakdown:

* **`PARTITION BY cid`** → Groups rows by customer ID
* **`ORDER BY price`** → Orders rows within each group
* **`ROWS BETWEEN 2 PRECEDING AND CURRENT ROW`** → Takes:

  * The current row
  * The **2 previous rows**
  * Calculates sum of `price` for them

🧠 Think of this as a **rolling window sum** within each customer's order history!

---

### 🖼️ Visualization Idea:

| cid | price | Running Sum (`2 PRECEDING` to `CURRENT`) |
| --- | ----- | ---------------------------------------- |
| A   | 10    | 10                                       |
| A   | 20    | 10 + 20 = 30                             |
| A   | 30    | 10 + 20 + 30 = 60                        |
| A   | 40    | 20 + 30 + 40 = 90                        |

---

## ➕ More Windowing Examples

### 1️⃣ Custom Ranges:

```sql
SELECT cid, SUM(price) OVER (
  PARTITION BY cid 
  ORDER BY price 
  ROWS BETWEEN 2 PRECEDING AND 3 FOLLOWING
) AS custom_sum
FROM orders;
```

* Includes 2 rows before and 3 after the current row in sum

---

### 2️⃣ Cumulative Sum:

```sql
SELECT cid, SUM(price) OVER (
  PARTITION BY cid 
  ORDER BY price 
  ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
) AS cumulative_sum
FROM orders;
```

* Adds all rows from the **start of partition** up to **current row**

---

## 💡 Benefits of Window Functions

✅ Do **not modify row structure**
✅ Great for **analytics and reporting**
✅ Replace complex subqueries
✅ Powerful alternative to self-joins or correlated queries

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

---

# **Hive File Formats & SerDe**

### 📂 **Hive File Formats**

Hive supports multiple file formats for storing data efficiently. Here are some of the popular ones:

1. **Text File**
   Simple line-by-line file storage (default format).

2. **SequenceFile**
   Binary file format for storing key-value pairs.

3. **RCFile (Record Columnar File)**
   A hybrid of row and column-based storage, improving query performance.

4. **ORC (Optimized Row Columnar) File**
   A columnar file format that is **highly optimized** for Hive's read and write operations. It improves performance by reducing I/O and supporting advanced compression techniques.

   **Example:**

   ```sql
   CREATE TABLE names 
   (fname string, lname string)
   STORED AS RCFile;
   ```

---

### 🔄 **Hive SerDe (Serializer/Deserializer)**

* **SerDe** is a mechanism used to convert between **Hive data** and the **storage format**.
* It controls how **records are read from** and **written to HDFS**.

#### Example of Using a SerDe:

```sql
CREATE TABLE emails (
   from_field string,
   sender string,
   email_body string
)
ROW FORMAT SERDE 
'org.apache.hadoop.hive.serde2.avro.AvroSerDe'
STORED AS INPUTFORMAT 
'org.apache.hadoop.hive.ql.io.avro.AvroContainerInputFormat'
OUTPUTFORMAT 
'org.apache.hadoop.hive.ql.io.avro.AvroContainerOutputFormat'
TBLPROPERTIES (
   'avro.schema.url' = 'hdfs://nn:8020/emailschema.avsc'
);
```

* Here, **AvroSerDe** is used to read/write Avro-formatted data.
* The **Avro schema** (`emailschema.avsc`) defines the structure of the data.

---

### 🗂️ **Using ORC Files in Hive**

The **ORC file format** is optimized for fast read/write operations and columnar storage.

#### Example of Creating a Table with ORC Format:

```sql
CREATE TABLE wh_visits_orc (
   lname string,
   fname string,
   time_of_arrival string,
   appt_scheduled_time string,
   meeting_location string,
   info_comment string
) STORED AS ORC;
```

* **ALTER TABLE** can also be used to change the storage format:

```sql
ALTER TABLE tablename SET FILEFORMAT ORC;
```

#### Default ORC Format Setting:

You can set ORC as the default file format for new tables:

```sql
SET hive.default.fileformat=Orc;
```

---

### 🧑‍💻 **Working with ORC Files in Hive**

After creating an ORC table, you can insert data and query it.

#### Insert Data:

```sql
INSERT INTO wh_visits_orc 
SELECT * FROM wh_visits;
```

#### Query Data:

```sql
SELECT * FROM wh_visits_orc LIMIT 10;
```

#### Checking ORC File Storage in HDFS:

Use the HDFS command to check the stored ORC files:

```bash
hdfs dfs -ls /user/hive/warehouse/wh_visits_orc;
```

---

# **Computing Table and Column Statistics in Hive**

### 📊 **Table Statistics**

You can compute statistics for a table to help the query optimizer make better decisions.

1. **Compute Statistics for a Table:**

   ```sql
   ANALYZE TABLE tablename COMPUTE STATISTICS;
   ```

2. **Compute Statistics for Specific Columns:**

   ```sql
   ANALYZE TABLE tablename COMPUTE STATISTICS FOR COLUMNS column_name_1, column_name_2, ...;
   ```

3. **Describe Formatted Table (Detailed Info):**

   ```sql
   DESCRIBE FORMATTED tablename;
   ```

4. **Describe Extended Table (Extended Info):**

   ```sql
   DESCRIBE EXTENDED tablename;
   ```

---

# **Vectorization in Hive**

### 🚀 **Vectorization + ORC Files = Improved Performance**

* **Vectorization** improves the performance of queries by enabling Hive to process **multiple rows** in a **single operation** (batch processing), rather than processing them one at a time.
* When used with **ORC files**, vectorization can lead to **significant performance improvements** in query execution.

---

# **Hadoop Limitations**

While Hadoop is a powerful tool for big data processing, it comes with several **limitations**:

### 1. **Unstructured Data**

* Hadoop stores **unstructured** data in HDFS, meaning there’s no predefined schema (like in traditional databases).
* HDFS stores data as **files** (text, log, audio, video, etc.), which are not structured in the same way databases store data in tables or rows.
* While structured formats like **CSV**, **XML**, and **JSON** can be stored in HDFS, Hadoop does not enforce any schema or constraints on these files.

### 2. **No Random Access**

* **Random access** (the ability to access and modify individual rows) is not possible in HDFS.
* **HDFS** is optimized for **storing large files** and **batch processing** them.
* You cannot modify a specific row in a file stored in HDFS without processing the entire file, making it unsuitable for **real-time** or **transactional systems**.

### 3. **High Latency**

* Hadoop processes data in **batch jobs** using **MapReduce**.
* This processing method can introduce **high latency**, as it may take **minutes or hours** to process large datasets, even with a large cluster.

### 4. **Not ACID Compliant**

* Hadoop is **not ACID compliant**, which means it doesn’t guarantee **Atomicity**, **Consistency**, **Isolation**, and **Durability** for transactions.
* In contrast, traditional relational databases are **ACID-compliant**, ensuring data consistency even during failures or concurrent operations.
* Hadoop does not provide the same transactional guarantees.


---

### 🧠 **ACID Properties in Databases**

Databases guarantee **ACID properties** to ensure data integrity. These properties make sure that transactions (operations on the database) are processed reliably and maintain the system's correctness. Let’s break down each property:

---

#### 🔄 **Atomicity**: "All or Nothing" 🛑

* **Definition**: A transaction must either be fully completed or not executed at all. If one part of the transaction fails, the entire transaction is rolled back to its original state.

* **Example**:
  Imagine you're withdrawing cash from an ATM. The operation has two main steps:

  1. **Update the cash balance** (the money in the ATM)
  2. **Update the account balance** (the amount in your bank account)

  If, for some reason, the ATM can't update your account balance but successfully dispenses cash, it would leave the system in an inconsistent state. **Atomicity** ensures that both actions happen together: either both are successful, or neither happens. If something fails, the transaction is canceled.

---

#### ⚖️ **Consistency**: "Data Validity" ✅

* **Definition**: Any changes made to the database must follow predefined rules, known as **constraints**, and must not leave the database in an inconsistent state.

* **Example**:
  Suppose there's a rule that a bank account balance can never be negative. If a transaction tries to reduce an account balance below zero, the **Consistency** property ensures that the change will not be allowed, keeping the data valid.

---

#### 🔒 **Isolation**: "Separation of Operations" 🏗️

* **Definition**: If multiple transactions are happening at the same time (concurrently), **Isolation** ensures that each transaction is processed as though it were the only one happening, preventing conflicts between them.

* **Example**:
  Imagine two people transferring money from the same bank account at the same time. If transaction A is subtracting \$100, and transaction B is adding \$50, isolation guarantees that each transaction will appear to run independently—one won’t interfere with the other. It’s like giving each person their own "turn" to interact with the account.

---

#### 🔒 **Durability**: "Permanent Changes" 📅

* **Definition**: Once a transaction is committed, the changes are permanent, even in the case of power outages or crashes. This ensures that after a successful transaction, the changes will survive and be available when the system restarts.

* **Example**:
  After a successful purchase on an e-commerce website, even if the website crashes or the system shuts down, the transaction (the purchase) will remain intact and visible when the system recovers.

---

### **Why ACID Matters**

ACID properties are crucial because they ensure **data reliability**, **accuracy**, and **consistency**, which is especially important in financial systems, e-commerce websites, and applications where transactions need to be processed correctly without loss of data.

---

These ACID properties lay the foundation for traditional relational databases, ensuring that transactions are processed reliably. However, in the world of **Big Data**, these strict guarantees might not always be feasible, leading to the use of more flexible, distributed systems. But understanding ACID helps you grasp the core principles of data integrity! 😎

---

### 🌐 **What is HBase?**

HBase is a **NoSQL database** built on top of Hadoop and designed for handling **large-scale, sparse** data across clusters. It’s a **distributed** column-family-based storage system that can store billions of rows and columns of data.

---

### 🧑‍💻 **HBase Commands**

Below are some important HBase-related commands:

#### 🏷️ **Basic Commands**:

* **`jps`**: Lists all the Java processes running on the system (HBase daemons included).

  * Example:

    ```bash
    jps
    ```

    Shows various processes like **HRegionServer**, **HMaster**, and **HQuorumPeer** (ZooKeeper).

* **HDFS Commands**:

  * **`hdfs dfs -ls /`**: List the contents of the HDFS root directory.
  * **`hdfs dfs -ls -R /`**: Recursively lists files and directories in HDFS.

  HBase directories in HDFS will be created like this:

  ```bash
  drwxr-xr-x   - talentum supergroup          0 2025-05-10 15:26 /hbase
  drwxr-xr-x   - talentum supergroup          0 2025-05-10 15:26 /hbase/.tmp
  drwxr-xr-x   - talentum supergroup          0 2025-05-10 15:26 /hbase/MasterProcWALs
  ```

---

### 🔧 **HBase Daemons**

When **HBase** is running, the following daemons are started:

1. **Zookeeper**: Manages coordination between different HBase instances.
2. **HBase Master Daemon**: Coordinates the region servers and handles cluster-wide actions.
3. **HBase RegionServer Daemon**: Manages the actual data (regions) in the table.

---

### 🖥️ **HBase Shell**

The **HBase Shell** is used to interact with HBase directly, similar to how we use the **Hive Shell** for Hive operations.

* **Command to enter HBase Shell**:

  ```bash
  bash run-hbase.sh -s start
  hbase shell
  ```

  * Once inside the shell, you can execute commands such as `put`, `get`, `list`, and more.

---

### 🏷️ **Table Structure in HBase**

In HBase, a **table** consists of **column families**. These column families group **related columns** together. Here are some important details:

* **Column Families**:

  * Each column belongs to one column family.
  * Example: If you have a `notifications` table, you might have two column families:

    * `attributes`: Holds data like `type`, `timestamp`.
    * `metrics`: Holds data like `#clicks`, `#views`.
* **Table Creation**:
  When creating a table, you must **define at least one column family**. You don’t need to specify individual columns when creating the table; they are defined dynamically when data is inserted.

---

### 💡 **Inserting Data in HBase**

In HBase, data is inserted **one cell at a time** using the **`put`** command. Here's an example:

* **Syntax**:

  ```bash
  put 'table_name', row_id, 'column_family:column_name', 'value'
  ```

* **Example**:
  Insert data into the `notifications` table:

  ```bash
  put 'notifications', 2, 'attributes:for_user', 'Chaz'
  ```

  * **Explanation**:

    * `'notifications'`: Table name
    * `2`: Row ID
    * `'attributes:for_user'`: Column family and column name
    * `'Chaz'`: Value inserted into the cell

  HBase tables are like a **sorted map**, where:

  * **Key**: column (with its column family)
  * **Value**: actual data (value)

---

### 🗃️ **Viewing Tables and Data**

* **List Tables**:
  To see a list of all HBase tables:

  ```bash
  list
  ```

* **Get Data**:
  Retrieve a cell value by using the `get` command:

  ```bash
  get 'notifications', 2
  ```

---

### 📝 **Summary**

* HBase is a **distributed** column-family-based NoSQL database.
* **Column families** are created during table creation, and individual columns are added dynamically.
* **Data insertion** in HBase is done one cell at a time, where each cell consists of a row ID, column family, column, and value.

---

### 🚀 **HBase in Action**

Once you've set up HBase and interacted with it via the shell, you'll notice that HBase’s architecture is optimized for storing **massive amounts of sparse data**, making it ideal for Big Data applications like storing logs, sensor data, or any other time-series data.

---


















