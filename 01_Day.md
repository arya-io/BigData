# 🧠 Big Data Ecosystem – Hadoop and Beyond

---

## 🚨 Big Data is a Problem, Hadoop is the Solution!

Big Data brings **challenges** like:
- Huge volumes of data
- Different types of data
- Fast data generation
- Difficulty in storing, processing & analyzing

That’s where **Hadoop** comes in – a **framework** designed to handle these challenges.

---

## 🏗️ Core Components of Hadoop

Hadoop mainly has **three parts**:

### 1. 🗄️ **Storage** – *HDFS (Hadoop Distributed File System)*
- Breaks huge files into **blocks**
- Distributes them across multiple computers (called **nodes**)
- Ensures **fault tolerance** by creating replicas

### 2. ⚙️ **Cluster Resource Management**
- Manages **coordination between storage & processing**
- Ensures every task knows where to go, what to do, and where to store results

### 3. 🧮 **Processing** – *MapReduce Framework*
- Written in **Java**
- Processes data in two steps:
  - **Map**: Break the problem into smaller chunks
  - **Reduce**: Combine the results

---

## ⚡ Why Spark over MapReduce?

While MapReduce is powerful, it has limitations:
- Only supports **Java**
- Slower due to multiple disk reads/writes

**Apache Spark** is a better choice:
- Supports **Java, Python, Scala, R**
- **Faster** in-memory processing
- Can handle:
  - ETL (Extract, Transform, Load)
  - Batch Processing
  - Real-time Streaming
  - Machine Learning

> **Spark = Everything MapReduce does, but faster + multi-language support + more features**

---

## 🐷 Apache Pig & Pig Latin

- **Pig** = Platform to process Big Data
- **Pig Latin** = Scripting language used in Pig
- Great for **ETL tasks**
- Higher-level abstraction over MapReduce
- Example: Easier syntax like SQL, instead of writing Java code

---

## 🧪 HBase – NoSQL Database

- HBase is a **distributed NoSQL database**
- Similar to **MongoDB** and **Cassandra**
- Stores data in **HDFS**
- **Built on top of Hadoop**
- Written in **Java**
- Cannot run **without Hadoop**
- Great for:
  - Handling **unstructured or semi-structured** data
  - Use cases needing **real-time read/write access**

---

## 🏢 Hive – The Data Warehouse

- Hive = **Data warehouse** tool built on top of Hadoop
- Converts **SQL-like queries** into **MapReduce jobs**
- Used for:
  - Storing **historical data**
  - Performing **analytical queries**

### 🧠 Difference between Databases & Data Warehouses:
| Feature | Database | Data Warehouse |
|--------|----------|----------------|
| Use | Daily operations | Analytical queries |
| Data Type | Current structured data | Historical structured data |
| Example | MySQL, Oracle | Hive, Amazon Redshift |

---

## 🔄 Apache Airflow – Workflow Orchestration

- Used to **automate data pipelines**
- Example Pipeline:
  1. **Data Cleansing** – e.g., remove spaces in names
  2. **Data Transformation** – split name into first and last
  3. **Data Analysis** – run insights

> All steps can be scheduled & managed using **Airflow DAGs (Directed Acyclic Graphs)**

Also achievable via:
- **Linux Cron jobs**
- **Shell scripting**
…but Airflow gives **better visualization, scheduling, and error handling**

---

## 🚀 Kafka – Real-Time Data Streaming

- **Messaging System** + **Streaming Platform**
- Moves data in **real-time** from one point to another
- Example Use Cases:
  - Uber’s live GPS tracking
  - Stock market tickers

### Important:
- Kafka **doesn't process** data
- It **delivers** data to processing tools like **Spark Streaming**

---

## 🧠 Summary

- **Hadoop** provides a full ecosystem for handling Big Data
- **Spark** is the next-gen processing engine: faster, flexible
- Tools like **Hive, Pig, HBase** simplify working with Big Data
- **Airflow** automates pipelines
- **Kafka** ensures real-time data flow

---

# 🔄 Data Science Life Cycle & Development Environment Basics

---

## 📈 Data Science Life Cycle – Step by Step

### 1. 🧠 **Business Understanding** *(Requirement Analysis Phase)*

- Ask **what problem** the client wants to solve
- Conduct **meetings with Domain Experts & Business Analysts**
- Define the **objective clearly**
- **No coding** is needed here — just **communication & planning**

> Example: “Can we predict customer churn?” — That’s the business question.

---

### 2. 🔍 **Data Mining** (Data Gathering)

- Provide a **POC (Proof of Concept)** to the client
- **Gather or scrape data** using tools like:
  - **Web Scraping**
  - **SQOOP** (Tool to import data from RDBMS to Hadoop)
- The data collected is usually **raw** and **unstructured**
  - Might contain: **NULL values, duplicates, inconsistencies**

---

### 3. 🧼 **Data Cleansing**

- Fix the issues in raw data:
  - Remove duplicates
  - Handle missing values (NULLs)
  - Correct data types
  - Standardize formats (e.g., date formats)

> Clean data = Reliable data for further analysis

---

### 4. 🔎 **Data Exploration & Feature Engineering**

- Understand the data by:
  - Viewing statistics (mean, min, max, etc.)
  - Creating graphs
- **Feature Engineering**:
  - Select important variables (features)
  - Create new features from existing ones

> Example: From “Date of Birth,” create “Age”

---

### 5. 🤖 **Predictive Modelling**

- Now comes **Machine Learning**!
- Apply algorithms like:
  - Decision Trees
  - Logistic Regression
  - Random Forest
- Train models using the cleaned and transformed data

---

### 6. 📊 **Data Visualization**

- Present your insights using:
  - **Graphs, charts, dashboards**
  - Tools: Matplotlib, Seaborn, Power BI, Tableau
- Communicate results clearly to:
  - **Stakeholders, Business Owners, Clients**

---

## ⚙️ Automation of the Process

- Steps **2, 3, 4** are part of **Data Engineering**
- Can be automated using:
  - **Linux Shell Scripts**
  - **Apache Spark**

---

## 🖥️ Understanding the Environment: Virtualization & OS

### 🪟 **Windows OS** = Host Machine

- This is your **main/physical system**
- On top of this, we use a **Hypervisor** to run virtual machines

### 📦 **Oracle VirtualBox** = Hypervisor

- It allows you to run **Virtual Machines (VMs)** within your system

### 💻 **Virtual Machines (Guest Machines)**

You are using:
- **Cloudera VM** – runs on **CentOS Linux**
- **BigDataVM** – runs on **Ubuntu (Debian-based Linux)**

These VMs are part of the **Development Environment**.

---

## 🏭 Real-World Setup

| Environment | Purpose | OS Used |
|-------------|---------|---------|
| **Development Environment** | Coding, testing, learning | Linux/Windows (your VMs) |
| **Production Environment** | Final deployment, real-time use | **Linux (99% cases)** |

> So, getting comfy with **Linux commands** is a must for Big Data & Data Science professionals!

---

# 📁 Edit Share Concept in VirtualBox – Linux File Access & Script Metadata

---

## 🧩 What is "Edit Share" in VirtualBox?

**Edit Share** in VirtualBox allows you to **share folders between your Host OS (Windows)** and **Guest OS (Linux VM)**.

Instead of uploading to cloud or transferring via USB, we directly access a **Windows folder from within Linux VM**.

---

### 🔧 How Does It Work?

- Linux uses **Mount Points** to access filesystems.
- **Mount Point**: A directory where an external file system (like Windows folder) is attached.
- In **VirtualBox**, we:
  - Go to VM Settings > Shared Folders
  - Set **Folder Path** to a Windows directory
  - Set **Mount Point** inside Linux VM (like `/home/talentum/shared/`)

> Mount points are **Linux-only concepts**, not native to Windows.

---

## 🖥️ Example Scenario – Sharing Data Between Host and VM

### 🧪 Terminal Checks

```bash
echo $HOME
# Output: /home/talentum

pwd
# Output: /home/talentum
```

This confirms your **current directory** inside the VM.

---

### 🗂️ Working with Files

1. **Download a ZIP file** on Windows.
2. **Extract it**, and place the contents into the **shared folder**.
3. Access this folder from inside BigDataVM.
4. Use **Linux command** to count lines in a CSV:

```bash
wc -l soccer_scores.csv | cat > count.txt
```

Or better:

```bash
wc -l soccer_scores.csv > count.txt
```

> ✅ The second command is more **efficient** because it directly writes the output to the file using **one process**.

---

### 📂 Copying Files to Shared Folder

To copy the result to shared folder:

```bash
cp ./count.txt ~/shared/
```

This makes `count.txt` visible on **Windows too!**

---

## ⚙️ File Type Recognition in Linux

When working with shell or Python scripts, Linux can **detect what type of file it is** using metadata.

### 🔍 Example: Using `file` Command

#### 1. **Shell Script with Shebang**

File: `copycommand.sh`

```bash
file copycommand.sh
# Output: Bourne-Again shell script, ASCII text executable
```

Means it’s a **bash script** because of the shebang line: `#!/bin/bash`

---

#### 2. **No Shebang**

File: `copycommand`

```bash
file copycommand
# Output: ASCII text
```

No shebang = just a regular text file (Linux won’t know how to execute it automatically)

---

#### 3. **Python Script**

Add this at the top of your Python file:
```python
#!/usr/bin/python
```

Then run:

```bash
file copycommand
# Output: Python script, ASCII text executable
```

> ✅ The `shebang` (`#!`) tells the OS **which interpreter to use** when running the file.

---

## 🧠 Bash Metadata Check

When you run a file in Linux, **bash** first checks:
1. Does the file have a **shebang** line?
2. What type of file is it? (shell, python, or plain text)
3. Can it be executed?

---

# 🏛️ Databases vs Data Warehouses vs NoSQL – OLTP vs OLAP Explained

---

## ⚙️ Fundamental Principles

| Type            | Principle      | Purpose                            |
|------------------|----------------|-------------------------------------|
| **Databases**     | OLTP (Online Transaction Processing) | Day-to-day operations |
| **Data Warehouses (like Hive)** | OLAP (Online Analytical Processing) | Forecasting, analytics |
| **NoSQL Databases** | OLAP or hybrid | Handle big volumes of unstructured or semi-structured data |

---

## 🗃️ Traditional RDBMS (Relational Databases)

- Data is organized in **tables** (also called **relations**).
- Follow strict **schemas** (predefined column structure).
- Work well for structured data, like:
  - Banking systems
  - Student databases
  - Ticket booking systems

> ✅ RDBMS uses **transactions** (COMMIT, ROLLBACK) to ensure consistency.

---

## 🔄 What is OLTP?

**OLTP (Online Transaction Processing)** is used for:
- Quick and **frequent transactions**
- Inserting, updating, deleting records
- Examples:
  - ATM withdrawal
  - Adding a product to cart
  - Submitting an online form

> These systems are called **Operational or Transactional Systems**

---

## 📊 What is OLAP?

**OLAP (Online Analytical Processing)** is used for:
- **Analyzing data** over time
- Supporting **business decisions**
- Generating reports, dashboards, forecasts

> Example: Analyzing sales data to forecast future revenue

---

## 🏢 Hive – The Data Warehouse

- Hive is a **Data Warehouse** built by **Facebook**
- Works on OLAP principle
- Provides SQL-like interface to query Big Data stored in **HDFS**
- Good for **Batch Processing**, not transactions

> Hive converts SQL queries into **MapReduce** jobs under the hood.

---

## 🌍 The Shift: From Relational Empire to Big Data

- **2008**: The birth of **NoSQL revolution**
  - Facebook open-sourced **Hive** (Data Warehouse)
  - Facebook also introduced **Cassandra** (NoSQL Database)
- Companies started shifting toward:
  - **Schema-free or Semi-structured data**
  - Flexible models: "Model as you go"

> Developers no longer want to define tables beforehand — data is growing too fast and too diverse!

---

## ⚔️ Operational Systems vs Data Warehousing

### 🏭 Operational Systems (OLTP):
- Built for **transactions** (insert, update, delete)
- Data changes frequently
- No integrated view (data comes from many sources)
- Not meant for long-term analysis
- Challenges:
  - No **uniform interface**
  - No centralized data
  - Hard to **share across departments**
  - Bad for **enterprise-wide decision making**

> Example: A banking system recording one transaction at a time.

---

### 🧠 Data Warehouses (OLAP):
- Built for **analysis, reporting, and forecasting**
- Acts as a **centralized repository**
- Stores **historical data** from multiple sources
- Provides a **homogenized view** of the organization

> Example: Analyzing 5 years of customer data to improve marketing.

---

### 💡 Forecasting = Predictive Modeling

- Once data is collected and stored in a Data Warehouse,
  we can use it for:
  - Forecasting sales
  - Predicting customer behavior
  - Analyzing trends over time

> And this is where **Machine Learning** can come into play!

---

# 🧠 What is Stored in a Data Warehouse? – Why OLAP Matters

---

## 📦 What Kind of Data Exists in a Data Warehouse?

A **Data Warehouse (DW)** holds a **centralized repository of cleaned, integrated, and historical data**, imported from various operational systems.

### ✅ Key Characteristics:
- **Read-only**: No editing or updating of data
- **Non-volatile**: Data doesn't change once loaded
- **Subject-oriented**: Organized by topics like Finance, HR, Sales, Research, etc.
- **Integrated**: Pulled from multiple sources, unified under a common schema

> Example: Data about student enrollments, alumni, financial reports — all stored in one place for analysis.

---

### 🔍 Compared to RDBMS (Traditional Database):

| Aspect                | RDBMS (OLTP)              | Data Warehouse (OLAP)               |
|------------------------|----------------------------|--------------------------------------|
| Purpose               | Transactions (Insert, Update, Delete) | Analysis, Reporting, Forecasting     |
| Data Scope           | Current data                | Historical + Current data            |
| Structure             | Application-specific        | Subject-oriented                     |
| Updates               | Frequently updated          | Read-only                            |
| Schema               | Normalized                  | Often Denormalized                   |
| Users                 | Clerical/Operational users  | Knowledge workers, Managers          |
| Data Format          | Encoded/Raw                 | Descriptive, Summarized + Detailed   |

---

## 🔗 What Does a Data Warehouse *Do*?

A Data Warehouse is not just storage — it's an **intelligent framework** that helps in:

### 🧩 Integration & Accessibility
- Combine data from different systems
- Make data accessible to **authorized users**

### 📊 Analysis & Reporting
- Enable **ad-hoc queries** and **deep analysis**
- Allow for **trend identification**, forecasts, and **data discovery**

### ♻️ Reusability
- Reuse cleaned data for **multiple business purposes**
- Build a long-term **data-driven strategy**

> It helps **managers and decision-makers** answer questions like:  
**"What were the most profitable products over the last 5 years?"**

---

## 🧑‍💼 Practitioner’s View of a Data Warehouse

> “A Data Warehouse is a **complete and consistent store** of data pulled from different sources and provided to users in a format they can easily understand and use in the business context.”

In short:
- It's not just about collecting data
- It's about **making sense** of it and **acting** on it

---

## 📐 Metadata & Schema in RDBMS

- In both **RDBMS and Data Warehouses**, schema defines the **structure** of the data
- But in **RDBMS**, it's **application-bound and strictly normalized**
- Schema = **Metadata**, i.e., *data about data* (like table structure, columns, data types)

---

## 📈 OLAP – Power Behind Business Intelligence (BI)

**OLAP (Online Analytical Processing)** powers many Business Intelligence (BI) tools and dashboards.

### 🔧 OLAP Capabilities:
- Multi-dimensional data views (slice and dice!)
- Fast **aggregation** (sum, average, count, etc.)
- “What-if” analysis for future planning (e.g., sales forecasts, budgets)

---

## ⚡ Why OLAP is Powerful

### ✅ Key Advantages:
- **Fast access** to large, multidimensional data
- **Complex calculations** on-the-fly
- Helps business leaders make **better, faster, and informed decisions**

> OLAP = The **brain** behind dashboards, reports, KPIs, and strategic insights.

---

# ✅ **Lesson Review – Data Warehousing & Introduction to Big Data**

---

### 1. **True or False**  
**The decision support wave introduced Online Analytical Processing (OLAP) and specialized DBMSs.**

✅ **True**  
> OLAP and specialized data management systems were introduced as part of the **decision support systems (DSS)** wave to help organizations **analyze data and make decisions**, not just perform transactions.

---

### 2. **Question:**  
**Which type of system acts as a centralized repository of an organization's data, ultimately providing a comprehensive and homogenized view of the organization?**

**✅ Answer:**  
**Data Warehouse**

> A **Data Warehouse** consolidates data from various sources, cleans and integrates it, and makes it ready for **analytics, forecasting**, and decision-making.

---

### 3. **Fill in the Blanks**  
**A fundamental axiom of the data warehouse is that the imported data is both __________ and ______________.**

**✅ Answer:**  
**Read-only** and **Non-volatile**

> Once data is loaded into a Data Warehouse, it's **not updated** or changed regularly like in OLTP systems. It remains **static** for consistent analysis.

---

### 4. **True or False**  
**A staging area is an intermediate storage area used for data processing during the extract, transform and load (ETL) process.**

✅ **True**  
> The **staging area** is a temporary storage zone used to **clean, transform**, and prepare raw data before loading it into the final Data Warehouse.

---

### 5. **State any advantage of OLAP Technology**

**✅ Answer:**  
**Fast access to multi-dimensional data for complex analysis and reporting.**

> OLAP supports:
- Real-time business intelligence
- Quick aggregations
- "What-if" scenario planning

---

# 🚀 Introduction to Big Data & Hadoop

---

## 📌 What Makes Data "Big Data"?

The term **Big Data** describes data that is **too large or complex** for traditional systems to handle effectively.

### Origin:
> Coined from **computational sciences**, Big Data emerged as a challenge of modern data processing.

---

## 🔑 The **3 Vs of Big Data** (Doug Laney, 2001)

| V | Description |
|--|-------------|
| **Volume**   | Massive amount of data (terabytes to petabytes and beyond) |
| **Velocity** | Data is generated and processed at high speed (real-time streaming) |
| **Variety**  | Data comes in multiple formats: structured (tables), semi-structured (XML, JSON), unstructured (videos, emails, images) |

> These three characteristics **overwhelm traditional databases**, and that’s where Big Data solutions like **Hadoop** come into play.

---

# **🌐 Big Data – The 3 V’s Explained**

---

## **🔑 What Are the 3 V’s of Big Data?**

Big Data isn’t just about having a lot of data — it’s about **how much**, **how fast**, and **how diverse** the data is.

### 📌 Defined by Doug Laney (2001):
> Big Data is best described using **three main characteristics**:
- **Volume**
- **Velocity**
- **Variety**

---

## **1️⃣ Variety – So Many Types!**

> Variety = **Different types and sources of data**

### 🔍 In Detail:
- Data comes in **various formats**:
  - **Structured**: Tables, rows, columns (like in databases)
  - **Semi-structured**: JSON, XML, CSV
  - **Unstructured**: Emails, PDFs, videos, social media posts, sensor logs

### ⚙️ Challenges:
- How to **gather, link, match, cleanse, and transform** these different types?
- How to **connect relationships and hierarchies** in data?
- Systems must be smart enough to make sense of this mix!

> **Example:** Imagine combining YouTube videos, Tweets, and Excel sheets into a single analysis.

---

## **2️⃣ Volume – Tons of Data!**

> Volume = **The amount of data being created and stored**

### 📊 Think:
- **Gigabytes, Terabytes, Petabytes... Zettabytes!**
- Coming from:
  - **Transactions** (banks, e-commerce)
  - **Social media feeds**
  - **Machine/sensor logs**

### 💸 Storage Cost Examples:
| Storage Type | Cost/GB |
|--------------|---------|
| SAN (Storage Area Network) | $2 – $10 |
| NAS (Network Attached Storage) | $1 – $5 |
| Local Storage | ~$0.05 |

### ⚠️ Challenges:
- Cost of storing huge data
- Filtering out **valuable** data from **junk**
- Processing it **fast enough** for decision-making

> **Example:** Storing all customer reviews across 5 years + analyzing them instantly.

---

## **3️⃣ Velocity – Speed of Creation**

> Velocity = **The speed at which new data is generated and moved**

### 🌀 Comes from:
- Social media
- Sensors (IoT devices)
- App logs
- GPS data
- RFID tags

### ⚠️ Challenges:
- Need to **react instantly** to avoid missing critical insights
- Dealing with **bursts or peaks** (e.g., festival season traffic on e-commerce sites)

> **Example:** Real-time fraud detection in credit card transactions.

---

## 🛠️ Designed for This: **Hadoop**

> “Big Data is high-volume, high-velocity, and high-variety information assets that demand **cost-effective**, **innovative** processing to enable enhanced insight and decision making.”  
> — *Gartner*

### ✅ Hadoop to the Rescue:
- Open-source framework made **specifically for Big Data**
- Handles **storage (HDFS)** and **processing (MapReduce/Spark)**
- Distributed across **multiple machines**, making it **scalable** and **affordable**

---

# **🐘 Apache Hadoop Overview**

---

## **What is Apache Hadoop?**

> **Apache Hadoop** is a:
- **Scalable**
- **Fault-tolerant**
- **Open-source** framework  
used for **distributed storage** and **processing of large datasets** on **commodity hardware**.

---

## **⚙️ Key Features of Hadoop**

### ✅ **1. Scalability**
- Hadoop can scale **from 1 to thousands** of machines (nodes).
- This is possible via **Hadoop Clusters**.
- **Production Environment** = Cluster-based setup.

> **Hadoop Admin** is responsible for setting up and maintaining this cluster.

---

### ✅ **2. Fault Tolerance**
- Hadoop achieves fault tolerance via **replication**.
- **Default replication factor**: 3 (can be configured).
- Even if a **DataNode** fails, the data isn't lost due to replicas.

---

## **Hadoop Architecture:**

### **1. HDFS (Hadoop Distributed File System)**

| Component     | Role |
|---------------|------|
| **NameNode** (Master) | Manages metadata, tells where to place blocks |
| **DataNode** (Worker) | Stores actual data blocks, handles replication |
| **Edge Node** (optional) | Acts as gateway in production |

> In **Development Environment**, the Edge Node is often on the same machine.

---

### **Block Distribution Process:**
1. **Client** contacts **NameNode** to write a file.
2. NameNode tells **how & where** to split into blocks.
3. **Client** breaks file into blocks, writes to DataNodes.
4. Each block is **replicated to 2 more DataNodes**.
5. **dfs.blocksize** decides block size (e.g. 128MB).
6. Replication managed via **dfs.replication** config.

---

### **Command Line Insight:**

#### `sudo jps`
- Lists all **Java processes** running on system.
- Shows:
  - **PID (Process ID)**
  - **Java class names**
- Helps monitor Hadoop components like:
  - NameNode
  - DataNode
  - SecondaryNameNode
  - ResourceManager, etc.

> `jps` = Java Virtual Machine Process Status Tool

---

## **How to Check Configuration:**

### Check Block Size and Replication Settings:
1. On Cloudera VM terminal, run:
   ```
   hadoop version
   ```
2. Visit:
   - [hadoop.apache.org](https://hadoop.apache.org)
3. Scroll to bottom → **Release Archive**
4. Select version → **Documentation**
5. Scroll sidebar → Click `hdfs-default.xml`
6. Search for:
   - `dfs.blocksize`
   - `dfs.replication`

---

## **Note:**
- In **Dev Environment**, `dfs.replication = 1` (only one machine).
- **Python**, **Java**, etc., can process **distributed data**.
- But **HDFS** does the actual job of **distributing data across nodes**.

---

# **🛠️ Apache Hadoop: Open Source & Distributed Processing**

---

## **What Does It Mean that Hadoop is Open Source?**
- **Apache Hadoop** is developed under the **Apache Software Foundation (ASF)**.
- It is **open source**, meaning:
  - **Freely available**
  - **Community-driven development**
  - **Licensing allows contributions, modifications, and use without cost**
- Anyone can:
  - **Add features**
  - **Fix bugs**
  - **Improve performance and scalability**

---

## **💾 Distributed Storage & Processing**

### **1. Distributed Storage:**
- Data is split into **blocks** and stored across multiple **DataNodes** in the cluster.
- Each node has:
  - Its **own RAM**
  - **Storage**
  - **Processor**

> **HDFS** handles the distribution of blocks.

---

### **2. Distributed Processing:**

#### **MapReduce:**
- Core component for **processing** large datasets in a distributed fashion.
- Written in **Java** and **Python**.
- **MapReduce = ETL Framework**  
  (Extract → Transform → Load)

---

## **⚙️ MapReduce Processing Flow**

| Phase       | Description |
|-------------|-------------|
| **Map**     | Processes input data into `<key, value>` pairs. One map task per Input Split. Runs **locally** on the DataNode holding the data block. |
| **Shuffle & Sort** | Intermediate `<key, value>` pairs are grouped by key and sent to the appropriate **Reducer**. |
| **Reduce**  | Aggregates values for each key and outputs final `<key, value>` results to **HDFS**. |

> Map and Reduce are **not daemons**, they are **per-application processes**.

---

## **Important Concepts**

- **Process** = Running instance of a program
- All processes in Hadoop are:
  - **Parallelized**
  - **Local to data (Data Locality)**

> This boosts performance by reducing network IO.

---

## **Key Takeaways**
- Hadoop’s distributed nature allows it to:
  - Store massive data reliably
  - Process it in parallel across nodes
- MapReduce always operates in **key-value pair** format
- It's powerful for **ETL jobs, analytics, and large-scale computation**

---

# **📦 Apache Hadoop on Commodity Hardware**

### **What is Commodity Hardware?**
- **Commodity hardware** refers to **inexpensive, off-the-shelf machines**.
- Hadoop runs on these to:
  - **Reduce hardware costs**
  - **Lower maintenance and support expenses**
- Hadoop’s architecture is designed for **scalability** and **fault tolerance**, making commodity hardware viable.

---

# **📊 Six Key Hadoop Data Types**

| Data Type | Description |
|-----------|-------------|
| **Sentiment** | Customer emotions from reviews, tweets, etc. |
| **Clickstream** | Website user navigation and actions |
| **Sensor/Machine** | Data from IoT devices, industrial machines |
| **Geographic** | Location-based data |
| **Server Logs** | Logs from web/app servers |
| **Text** | Unstructured data like emails, web pages, documents |

---

## **Use Case: Sentiment Analysis for Iron Man 3**

### **Goals:**
- Analyze sentiment around the movie’s release.
- Determine public opinion **before and after** debut.

### **Example Tweets:**
- *"Iron Man 3 was awesome!"*
- *"Tony Stark has 42 suits!"*
- *"Thor was way better than Iron Man 3"*

---

## **📥 Getting Twitter Data into Hadoop**
### **Tool: Apache Flume**
- **Flume** captures real-time streaming data (like tweets) and pushes it into **HDFS**.

---

## **Use HCatalog to Define Schema**
```sql
CREATE EXTERNAL TABLE tweets_raw (
  id BIGINT,
  created_at STRING,
  source STRING,
  favorited BOOLEAN,
  retweet_count INT,
  text STRING
);
```

---

## **📈 Visualizing Data**

- **Spikes in Tweet Volume**: Bar Graph  
  - Notable spikes on *Thursday midnight*, *Friday evening*, *Saturday showtimes*.

- **Sentiment by Country**: Geo-Map  
  - Ireland: 50% Positive  
  - Mexico: 67% Neutral

---

## **Use Case: Geolocation in Trucking**

### **Goals:**
- **Reduce fuel costs**
- **Improve driver safety**

### **Example Data Format:**

| truckid | driverid | event | lat | lon | city | state | velocity | event_indicator | idling_indicator |
|---------|----------|-------|-----|-----|------|-------|----------|------------------|------------------|
| A5 | A5 | unsafe following distance | 41.52 | -124.03 | Klamath | CA | 33 | 1 | 0 |

> Hadoop can only process this data **once it is in HDFS**.  
**Flume** is used to **stream sensor data into Hadoop.**

---

# **🚛 Truck Data in Hadoop**

## **RDBMS Truck Data Schema**
- The original data is stored in an **RDBMS** and includes:
  - `driverid`, `truckid`, `model`
  - `monthyear_miles`, `monthyear_gas`
  - `total_miles`, `total_gas`, `mileage`
- Data goes back to **2009**.

---

## **📤 Getting RDBMS Data into Hadoop**
### **Tool: Apache Sqoop**
- **Sqoop** is used to **import/export data between RDBMS and Hadoop**.
- It transfers structured data into **HDFS** for further processing.

---

## **🗃 HCatalog: Shared Schema Layer**

### **Schema Definitions:**
```sql
CREATE TABLE trucks (
  driverid STRING,
  truckid STRING,
  model STRING,
  monthyear_miles INT,
  monthyear_gas INT,
  total_miles INT,
  total_gas DOUBLE,
  mileage DOUBLE
);

CREATE TABLE events (
  truckid STRING,
  driverid STRING,
  event STRING,
  latitude DOUBLE,
  longitude DOUBLE,
  city STRING,
  state STRING,
  velocity DOUBLE,
  event_indicator BOOLEAN,
  idling_indicator BOOLEAN
);

CREATE TABLE riskfactor (
  driverid STRING,
  riskfactor FLOAT
);
```

---

## **❓ Data Analysis Goals**
1. **Which trucks are wasting fuel through unnecessary idling?**
2. **Which drivers are most frequently involved in unsafe events on the road?**

---

## **🧮 Using Hive for Analysis**

### **Compute Truck Mileage**
```sql
CREATE TABLE truck_mileage AS
SELECT
  truckid,
  rdate,
  miles,
  gas,
  miles/gas AS mpg
FROM trucks
LATERAL VIEW stack(
  54,
  'jun13', jun13_miles, jun13_gas,
  'may13', may13_miles, may13_gas,
  'apr13', apr13_miles, apr13_gas,
  ...
) dummyalias AS rdate, miles, gas;
```

- `stack()` is used to **unpivot** the monthly data into rows.
- This makes it easier to compute and analyze **mileage per gallon (mpg)**.

---

# **🐷 Pig Script for Computing Risk Factor**

## **Script Overview:**
```pig
-- Load events data from HCatalog
a = LOAD 'events'
    USING org.apache.hive.hcatalog.pig.HCatLoader();

-- Filter out 'Normal' events
b = FILTER a BY event != 'Normal';

-- Create occurrence record per driver/event
c = FOREACH b GENERATE driverid, event, (int)'1' AS occurance;

-- Group by driver to get total occurrences
d = GROUP c BY driverid;
e = FOREACH d GENERATE group AS driverid, SUM(c.occurance) AS t_occ;

-- Load truck data from HCatalog
f = LOAD 'trucks'
    USING org.apache.hive.hcatalog.pig.HCatLoader();

-- Extract total miles from two months
g = FOREACH f GENERATE driverid, ((int) apr09_miles + (int) apr10_miles) AS t_miles;

-- Join events and trucks data on driverid
join_d = JOIN e BY driverid, g BY driverid;

-- Compute risk factor: (unsafe events / miles) * 1000
final_data = FOREACH join_d GENERATE
    $0 AS driverid,
    (float) $1 / $3 * 1000 AS riskfactor;

-- Store result into HCatalog table
STORE final_data INTO 'riskfactor'
    USING org.apache.hive.hcatalog.pig.HCatStorer();
```

- **Risk Factor** = Number of Unsafe Events per 1000 Miles
- Final output is stored in the `riskfactor` table in HCatalog
- Risk factors can be visualized on a **geolocation map**

---

# **🧩 Hadoop Ecosystem Project**
Hadoop Core Components:
- **HDFS** – Storage layer
- **MapReduce** – Processing engine
- **YARN** – Resource management

Ecosystem Tools:
- **Sqoop** – Import/Export data from RDBMS
- **Flume** – Stream data into Hadoop (e.g., from Twitter)
- **Hive** – SQL-like interface for querying data
- **Pig** – Scripting language for data flow
- **Spark** – In-memory distributed processing

---

# **⚖️ RDBMS vs. Hadoop**

| Feature                        | RDBMS                         | Hadoop                                 |
|-------------------------------|-------------------------------|----------------------------------------|
| **Schema**                    | Required on write             | Required on read                       |
| **Speed**                     | Fast reads                    | Fast writes                            |
| **Structure**                 | Strictly structured           | Loosely structured                     |
| **Processing**                | Coupled with data             | Decoupled; uses external engines       |
| **Data Types**                | Structured only               | Structured, semi-structured, unstructured |
| **Best Use Case**             | OLAP, ACID Transactions       | Data Discovery, Big Data processing    |
| **Integration**              | Standalone                    | Works *alongside* RDBMS                |

---

# **About Hadoop 2.x**

## **Core Modules in Hadoop 2.x**
1. **Hadoop Common**: Utility functions and libraries supporting all Hadoop modules.
2. **HDFS**: Hadoop Distributed File System for scalable, redundant storage.
3. **YARN**: Yet Another Resource Negotiator – handles **job scheduling** and **resource management**.
4. **MapReduce**: Framework for distributed **data processing**.

---

## **Hadoop 1.x vs Hadoop 2.x Architecture**

| Feature | Hadoop 1.x | Hadoop 2.x |
|--------|-------------|-------------|
| **Resource Management** | MapReduce (tightly coupled with data processing) | **YARN** (decoupled from MapReduce) |
| **Data Processing** | MapReduce only | MapReduce + Others (e.g., Spark, Tez) |
| **Storage** | HDFS | HDFS |
| **Scalability & Flexibility** | Limited | Greatly improved |

### Key Change:
- **YARN introduced** to separate **resource management** from **data processing**, enabling **multiple applications** to run concurrently on the same cluster.

---

## **YARN Components (Daemons)**:
- **ResourceManager (Master)**: Manages allocation of cluster resources.
- **NodeManager (Worker)**: Manages resources and reports to ResourceManager.

## **HDFS Components (Daemons)**:
- **NameNode (Master)**: Manages metadata and namespace.
- **DataNode (Worker)**: Stores actual data blocks and replicates them.

---

# **The Hadoop Ecosystem**

### **Core:**
- **HDFS** + **MapReduce** + **YARN**

### **Data Ingestion & Integration:**
- **Sqoop** – Import/export from RDBMS
- **Flume** – Stream data into Hadoop

### **Data Processing & Scripting:**
- **Pig** – Data flow scripts
- **Hive** – SQL-like query interface
- **Spark** – In-memory processing engine (Unified platform)
- **Storm** – Real-time computation

### **Workflow & Monitoring:**
- **Oozie** – Workflow scheduler
- **Apache Ambari** – Cluster management and monitoring

### **Storage/Query Engines:**
- **HBase** – NoSQL database
- **Accumulo** – Secure key/value store
- **Apache Solr** – Full-text search engine

### **Metadata & Governance:**
- **Apache Falcon** – Data governance & lineage
- **HCatalog** – Table and schema management for Hive

### **Coordination & Machine Learning:**
- **ZooKeeper** – Distributed coordination
- **Mahout** – Machine learning (written in Java)

---

## **Why Spark is a Unified Platform?**
- Spark can **replicate functionalities** of:
  - **Pig** (Data transformations)
  - **Hive** (SQL queries)
  - **Storm** (Streaming)
  - **Mahout** (ML algorithms)
- Supports **batch**, **streaming**, **SQL**, and **machine learning** workloads – all on one engine.

---

# **Hadoop Deployment Modes**

## **1. Standalone Mode**
- **Single system installation**
- All Hadoop daemons run in **one Java Virtual Machine (JVM)**
- Uses the **local file system** (not HDFS)
- **Best for**:
  - Testing
  - Development
  - Introductory training

---

## **2. Pseudo-Distributed Mode**
- Still a **single system** installation
- Each Hadoop daemon runs in its **own JVM**
- Uses **HDFS** (but still on local disks)
- **Best for**:
  - QA (Quality Assurance)
  - Development/testing environments
  - Used in **Hortonworks Sandbox**

---

## **3. Distributed Mode**
- **Multi-system installation**
- Each daemon runs in its **own JVM**, possibly multiple per machine
- Uses **HDFS distributed across multiple systems**
- **Best for**: **Production environments**

---

# **Lesson Review**

### **Q: What are 1,024 petabytes known as?**
- **Answer**: 1 **Exabyte**

### **Q: What are 1,024 exabytes known as?**
- **Answer**: 1 **Zettabyte**

### **Q: List the three Vs. of big data**
- **Volume**
- **Velocity**
- **Variety**

### **Q: Sentiment is one of the six key types of big data. List the other five.**
1. Clickstream  
2. Sensor/Machine  
3. Geographic  
4. Server Logs  
5. Text

### **Q: What technology might you use to stream Twitter feeds into Hadoop?**
- **Flume**

### **Q: What technology might you use to define, store, and share the schemas of your big data stored in Hadoop?**
- **HCatalog**

### **Q: What are the two main new components in Hadoop 2.x?**
1. **YARN**
2. **(Second)**: **Decoupled MapReduce engine** (separate from resource management)

---

# **Lab Commands and Utilities**

### **Basic HDFS/Admin Tools**
- `hdfs dfsadmin -report` → Reports HDFS health and usage
- `hdfs dfs -ls /` → List files in root of HDFS

### **System Utilities**
- `echo $HOSTNAME` → Show hostname (useful for identifying DataNodes)
- `sudo jps` → Lists running Java processes (NameNode, DataNode, etc.)
- `sudo netstat -nputl | grep PID` → View network usage and PID details

### **Important Ports**
- **8088** → YARN ResourceManager (Web UI)
- **50070** → NameNode Web UI (for HDFS file browser)

---

# **Command Categories in Hadoop**

### **1. User Commands**
- Used for **file system operations**
- Examples: `ls`, `put`, `get`, `cat`, etc.

### **2. Admin Commands**
- Used for **cluster-level tasks and monitoring**
- Examples: `dfsadmin`, `balancer`, etc.

### **3. File System Check (fsck)**
- Used to check **health of HDFS**
- Detects **missing/corrupt blocks**

---
