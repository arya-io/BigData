# 🔍 What is Big Data?  
Big Data refers to extremely large and complex datasets that traditional data-processing software struggles to handle. It involves storing, processing, and analyzing huge amounts of information efficiently.  

📖 *Definition:* “Big data is a term used to refer to the study and applications of data sets that are too complex for traditional data-processing software.” – Wikipedia  

---

# 📊 The Three V's of Big Data  
Big Data is characterized by three main factors:  

- **📦 Volume:** The size of the data (huge amounts of information collected from various sources).  
- **🌍 Variety:** The different formats and types of data (structured, semi-structured, and unstructured).  
- **⚡ Velocity:** The speed at which data is generated, processed, and analyzed.  

💡 *Example:* Think of social media—millions of users generate posts, comments, and messages every second. This enormous, fast-moving, and diverse data is classic Big Data!  

---

# 🖥️ Big Data Concepts & Terminology  

- **🖥️ Clustered Computing:** Using multiple machines together to form a powerful system.  
- **🔄 Parallel Computing:** Performing computations simultaneously to speed up processing.  
- **🌐 Distributed Computing:** Multiple networked computers work together, sharing the workload.  
- **📦 Batch Processing:** Dividing large jobs into smaller chunks and running them separately.  
- **⚡ Real-Time Processing:** Handling data instantly as it arrives (e.g., stock market updates).  

💡 *Example:* Online transactions—when you make a purchase, the system instantly processes payment details, checks availability, and confirms your order.  

---

# ⚙️ Big Data Processing Systems  

### 🔹 Hadoop/MapReduce  
- ✔️ A scalable, fault-tolerant framework written in Java.  
- 🔓 Open-source, widely used in Big Data.  
- ⏳ Primarily supports batch processing (processing data in chunks).  

### ⚡ Apache Spark  
- 🚀 A high-speed, general-purpose cluster computing system.  
- 🔓 Open-source, like Hadoop.  
- 🏎️ Supports both batch and real-time data processing, making it more versatile.  

💡 *Comparison:* Hadoop works like a traditional assembly line, processing one batch at a time. Spark, on the other hand, processes data much faster and supports real-time tasks!  

---

# ⚡ Features of Apache Spark  

- 🌐 **Distributed computing framework** – Runs efficiently across multiple machines.  
- 🔥 **In-memory computations** – Stores intermediate results in RAM for ultra-fast performance.  
- 🏎️ **Lightning-fast processing** – Executes tasks much quicker than traditional systems.  
- 🔣 **Multi-language support** – Works with Java, Scala, Python, R, and SQL.  
- ⚡ **Always faster than MapReduce** – Uses optimized memory management for speed.  

💡 *Example:* If Hadoop is a truck carrying data from one place to another, Spark is a high-speed bullet train that gets the job done in record time! 🚄  

---

# 🔥 Apache Spark Components  

![image](https://github.com/user-attachments/assets/4a5d8342-4251-45ce-9efc-12f3563b7965)  

Apache Spark consists of several components that enhance its functionality:  

- **🗂️ Spark SQL** – Used for structured data processing, similar to SQL databases.  
- **🤖 MLlib (Machine Learning Library)** – Provides algorithms for machine learning tasks like classification, clustering, and regression.  
- **🔗 GraphX** – Optimized for graph-based computations and analytics (think social network connections).  
- **🌊 Spark Streaming** – Handles real-time data processing, such as analyzing live tweets or stock prices.  
- **⚡ RDD API (Resilient Distributed Dataset)** – The core data model of Spark, just like:  
  - Tables in Hive  
  - Relations in Pig  
  - DataFrames in Pandas  

💡 *Example:* If you’ve ever worked with Pandas in Python, RDDs are somewhat similar—they provide a flexible way to process data across multiple machines!  

---

# 🚀 Spark Modes of Deployment  

Spark can run in different modes depending on the environment:  

- **💻 Local Mode** – Runs on a single machine, like your laptop.  
  - ✅ Best for testing, debugging, and small-scale experiments.  
  - ✅ Convenient for learning and demonstrations.  

- **🌐 Cluster Mode** – Runs on a group of predefined machines in a distributed setup.  
  - ✅ Used for production environments.  
  - ✅ Handles large-scale data efficiently.  

🔄 **Workflow:**  
Development starts on **Local Mode**, and then moves to **Cluster Mode** for production—without requiring any code changes!  

💡 *Example:* Think of Local Mode as using your laptop for practice, while Cluster Mode is like deploying an app on powerful servers for real-world users.  

---

# 🐍 PySpark  

## 🚀 PySpark: Spark with Python  

Apache Spark is originally written in Scala, but to enable Python developers to use Spark, the community introduced **PySpark**!  

### ⚡ Features of PySpark:  
- ✅ Provides the same **speed** and **power** as Scala-based Spark.  
- ✅ PySpark APIs are **similar to Pandas and Scikit-learn**, making it beginner-friendly.  

💡 *Example:* If you already use Pandas for data analysis, switching to PySpark for big data tasks will feel natural!  

---

# 🏗️ What is Spark Shell?  

Spark Shell is an interactive environment where you can quickly execute Spark jobs. It helps in:  

✔️ **Fast prototyping** – Quickly testing whether something works or not.  
✔️ **Interacting with data** – Directly working with files on disk or data in memory.  

### 🖥️ Types of Spark Shells:  
- 🟠 **Spark-shell** for Scala  
- 🔵 **PySpark-shell** for Python  
- 🟢 **SparkR** for R  

🔹 Spark can also run in **Java**, but there is **no dedicated shell for Java**.  

💡 *Example:* Think of Spark Shell as a Python REPL (interactive prompt), but for big data processing—it allows you to run small code snippets and experiment with Spark's capabilities without setting up full programs!  

---

# 🛠️ Opening Python Shell Using PySpark  

You can open the **Python shell using PySpark** instead of Jupyter Notebook by running the following command in your terminal:  

```bash
pyspark
```

This will launch the PySpark interactive shell, allowing you to run Spark commands directly.  

💡 *Example:* If you're familiar with Python's interactive prompt (`python` command in the terminal), PySpark works similarly but with Spark-based functions included!  

---

To run **PySpark** in the **Python shell** instead of launching Jupyter Notebook, you need to unset certain configurations. Here’s how you can do it:  

### 🛠️ Steps to Unset the Configuration & Use Python Shell  

1️⃣ **Unset the `PYSPARK_DRIVER_PYTHON` and `PYSPARK_DRIVER_PYTHON_OPTS` environment variables**  
Run the following command in your terminal:  

```bash
unset PYSPARK_DRIVER_PYTHON
unset PYSPARK_DRIVER_PYTHON_OPTS
```

🔹 These environment variables are responsible for launching Jupyter Notebook by default when you run `pyspark`.  

2️⃣ **Run PySpark in the Terminal**  
Once the configurations are unset, simply enter:  

```bash
pyspark
```

✔️ This will now open the **PySpark interactive shell**, instead of Jupyter Notebook.  

💡 *Example:* Think of this like switching from a **fancy graphical interface (Jupyter)** to a **raw terminal experience**, where you can directly run Python commands with Spark.  

---

## 🚗 **Understanding SparkContext**

### What is SparkContext?

SparkContext is the **entry point** to the world of **Apache Spark**. 🌟

* Think of it like a **key** to a **house**. You need this key to access the Spark functionalities (like opening the door to the house). 🏠
* In **PySpark**, the default **SparkContext** is named **sc**. PySpark automatically creates this for you when you start working in the PySpark shell, so you don’t need to create it yourself.

### Analogy to Make It Easier

* Imagine SparkContext as the **key** to your **car** 🚗. Without it, you can't drive or interact with the car (Spark). PySpark gives you the key (SparkContext) so you can start driving (running your Spark jobs).

---

### Example: Accessing SparkContext Information

Let’s check out a simple **script.py** to learn more about **SparkContext**.

```python
# Print the version of SparkContext
print("The version of Spark Context in the PySpark shell is", sc.version)

# Print the Python version of SparkContext
print("The Python version of Spark Context in the PySpark shell is", sc.pythonVer)

# Print the master of SparkContext
print("The master of Spark Context in the PySpark shell is", sc.master)
```

* **Output**:

  ```bash
  The version of Spark Context in the PySpark shell is 2.4.5
  The Python version of Spark Context in the PySpark shell is 3.6
  The master of Spark Context in the PySpark shell is local[*]
  ```

In the example:

* **sc.version** gives the Spark version.
* **sc.pythonVer** shows the Python version used with Spark.
* **sc.master** tells you whether Spark is running locally or on a cluster.

---

## 🔍 **Inspecting SparkContext**

If you want to inspect your **SparkContext**, you can run a few commands:

```python
# Check the ID of the SparkContext
id(sc)  # This will give you a unique ID for the SparkContext

# Check the type of SparkContext
type(sc)  # <class 'pyspark.context.SparkContext'>

# Check SparkContext version
sc.version  # Example output: '2.4.5'

# Check Python version
sc.pythonVer  # Example output: '3.6'

# Check the master
sc.master  # Example output: 'local[*]'
```

### Example Output:

```bash
id(sc)
139771463232984

type(sc)
<class 'pyspark.context.SparkContext'>

sc.version
'2.4.5'

sc.pythonVer
'3.6'

sc.master
'local[*]'
```

---

## 📥 **Loading Data in PySpark**

You can load data into PySpark using the **SparkContext** methods.

### 1. **parallelize() Method**

* This method is used to **create an RDD** (Resilient Distributed Dataset) from a list or collection.

  Example:

  ```python
  rdd = sc.parallelize([1, 2, 3, 4, 5])
  ```

  Here, we parallelize a list of numbers, which will allow us to process them in parallel across multiple Spark workers.

### 2. **textFile() Method**

* This method is used to **load a text file** into an RDD.

  Example:

  ```python
  rdd2 = sc.textFile("test.txt")
  ```

  This will read the **test.txt** file and create an RDD from it, which can be processed by Spark.

### File Protocols

In **Jupyter Notebooks**, you're not working in a Spark shell. However, you can still execute Spark commands and interact with Spark via **PySpark** in a notebook environment. 📝

---

### 🧠 **Quick Recap**:

* **SparkContext** is your **entry point** to using **Apache Spark**.
* **parallelize()** and **textFile()** are common methods to load data into Spark.
* You can easily inspect the version, Python version, and cluster information using `sc.version`, `sc.pythonVer`, and `sc.master`.

---

## 🖥️ **Interactive Use of PySpark**

### What is the PySpark Shell?

PySpark comes with its own **interactive Python shell**. Think of this shell as a **playground** for testing and experimenting with Spark operations. 🛠️

* The shell comes with **PySpark already installed**, making it very convenient for **basic testing and debugging**. You don't need to worry about setting things up manually!
* One of the coolest things? You don't have to create a **SparkContext object** yourself. **PySpark** automatically creates a **SparkContext**, and it’s available by default as the variable `sc`. This saves you a lot of time! ⏱️

---

### Example: Working with PySpark Shell

Let’s see how we can use the **PySpark shell** to work with data:

```python
# Create a Python list of numbers from 1 to 100
numb = range(1, 101)
print(type(numb))  # <class 'range'>

# Load the list into PySpark
spark_data = sc.parallelize(numb)
print(type(spark_data))  # <class 'pyspark.rdd.RDD'>

# Collect the data and print it
print(spark_data.collect())  # Prints all the numbers in the list

# Get help on the collect method
help(spark_data.collect())
```

### Key Points:

* **parallelize()**: This method is used to convert a regular Python list (like `numb`) into a **distributed collection** in Spark (an RDD). 🧑‍💻
* **collect()**: This gathers the data back to the driver and prints it, but be careful – for very large datasets, this could overload your memory. 😅

---

## 📂 **Loading Data in PySpark Shell**

In PySpark, data is processed through **distributed collections** (like RDDs). These collections are automatically **parallelized** across the cluster, so you don’t need to worry about manually splitting the data. 💥

### Example: Loading a Local File into PySpark

Let’s load a file into PySpark using the `textFile()` method. Here's how:

```python
# Define the file path
file_path = 'file:////home/talentum/spark/README.md'

# Load the file into PySpark
lines = sc.textFile(file_path)

# Print the first 5 lines of the file
print(lines.take(5))
```

### Output:

```bash
['# Apache Spark', '', 'Spark is a fast and general cluster computing system for Big Data. It provides', 'high-level APIs in Scala, Java, Python, and R, and an optimized engine that', 'supports general computation graphs for data analysis. It also supports a']
```

### Understanding the Methods:

* **take(5)**: This gets the **first 5 lines** of the file (like reading the first few lines of a book). 📖

  * `lines.take(5)` returns a **list**: `['line 1', 'line 2', ...]`
* **first()**: If you only want the very first line, you can use this method:

  ```python
  lines.first()  # Returns the very first line
  ```

### Types of Output:

```python
# Checking the types
print(type(lines.take))  # <class 'method'>
print(type(lines.take(5)))  # <class 'list'>
print(type(lines.first()))  # <class 'str'>
```

In **RDDs**, every line in the file is considered an **element** of the RDD. Think of an RDD as a collection of **lines of text** or **data records** that can be processed in parallel.

---

### 🧠 **Quick Recap**:

* The **PySpark shell** is great for testing and debugging because it comes with PySpark pre-installed and automatically creates a `SparkContext` for you.
* You can **parallelize** your data and run operations like **collect()** or **take()** to inspect the data.
* Data is represented as **RDDs** in PySpark, and you can load files using **textFile()** and perform operations on them.

---

## 🧑‍💻 **Use of Lambda Function in Python - filter()**

### What are Anonymous Functions in Python? 🤔

In Python, **lambda functions** are **anonymous functions**. This means they don't have a name like regular functions created with `def`. Instead, they are used for **short, simple tasks** where defining a full function would be overkill. 🎯

Lambda functions are:

* **Powerful**: You can use them in combination with functions like **map()** and **filter()**.
* **Efficient**: They let you write **concise** code for simple operations.

They allow you to create a function on the fly, and it gets executed later. Think of them like **mini functions** that you don’t need to give a name to!

---

## 📝 **Lambda Function Syntax**

A **lambda function** in Python follows this basic syntax:

```python
lambda arguments: expression
```

### Example:

```python
# Lambda function to double a number
double = lambda x: x * 2
print(double(3))  # Output: 6
```

Here:

* `lambda x: x * 2` creates an anonymous function that takes `x` and returns `x * 2`.
* It is similar to writing a `def` function but in a **one-liner**.

---

## 🆚 **Difference Between def and lambda Functions**

Both `def` and `lambda` functions are used to create functions in Python, but there are some key differences:

### Example: Cube of a Number

```python
# Using def to create a function
def cube(x):
    return x ** 3

# Using lambda to create a function
g = lambda x: x ** 3

print(g(10))   # Output: 1000
print(cube(10))  # Output: 1000
```

### Key Differences:

* **Return statement**: Lambda functions do not explicitly require the `return` keyword.
* **Location**: You can place lambda functions **anywhere** in your code (inline), whereas `def` functions need to be defined before use.

---

## 🔄 **Use of Lambda Function in Python - map()**

The `map()` function in Python applies a **function** to all items in a list (or another iterable) and returns a new list with the results. You can use **lambda functions** inside `map()` for a concise, efficient solution. 🧠

### General Syntax of `map()`:

```python
map(function, iterable)
```

### Example of `map()`:

```python
# Add 2 to each element of the list
items = [1, 2, 3, 4]
result = list(map(lambda x: x + 2, items))
print(result)  # Output: [3, 4, 5, 6]
```

### Why Use map()?

The `map()` function eliminates the need for a **for loop**, making the code more **concise** and **easier to read**. Instead of writing a long loop, you can achieve the same result in a single line.

---

## 🔎 **Use of Lambda Function in Python - filter()**

The `filter()` function in Python is used to **filter** elements from a list based on a condition provided by a function. You can combine **filter()** with **lambda functions** to create **inline filters** that select specific items from the list. 🧹

### General Syntax of `filter()`:

```python
filter(function, iterable)
```

### Example of `filter()`:

```python
# Filter out even numbers, keep odd numbers
items = [1, 2, 3, 4]
result = list(filter(lambda x: (x % 2 != 0), items))
print(result)  # Output: [1, 3]
```

Here:

* The lambda function checks if a number is **odd** (i.e., `x % 2 != 0`).
* `filter()` only keeps the numbers where the condition evaluates to **True**.

---

## 🚫 **Lambda Functions Are Not a Feature of Spark**

Although **lambda functions** are **great** for data manipulation in Python, **Spark** does not directly use lambda functions for its core operations. However, you can use lambda functions in **PySpark** for some data transformations when working with RDDs or DataFrames. 🧑‍💻

---

### 🧠 **Quick Recap**:

* **Lambda functions** are **anonymous** functions that can be used inline to simplify your code.
* **map()** applies a function to every item in a list, and **filter()** filters items based on a condition.
* These functions allow for **concise** and **efficient** code when handling lists or iterables in Python.

---

📌 **Understanding RDD (Resilient Distributed Datasets) in Apache Spark** ⚡

![image](https://github.com/user-attachments/assets/4748b963-20e5-4cdd-a64f-fdc403ed6444)


RDD is the **fundamental building block** of Apache Spark, enabling distributed data processing with fault tolerance. Let’s break it down in simple terms! 😊  

---

### 🔍 **What is an RDD?**  
**Resilient Distributed Dataset (RDD)** is a **distributed collection of data** that is **fault-tolerant** and allows parallel processing across multiple nodes in a cluster.  

Think of an RDD like a **large dataset split into smaller chunks** and spread across multiple computers for efficient processing! 🚀  

---

### 🖥️ **How RDD Works**  
1️⃣ The **Spark driver** reads data from a source like HDFS, local files, or databases.  
2️⃣ It **splits the data into multiple partitions** and distributes them across nodes in the cluster.  
3️⃣ Each partition is **processed in parallel**, making computations much faster! 💡  

📜 **Example Code to Create an RDD:**  
```python
rdd = sparkContext.textFile("hdfs://data/sample.txt")
```
✅ This loads a text file as an RDD, which Spark processes in chunks across nodes.  

---

### 📷 **Visual Representation**  
Your image illustrates this well:  
- The **Spark driver reads data** from a file on disk.  
- It **creates an RDD** and distributes the partitions across nodes in the cluster.  
- Each node processes its **RDD partition independently**, ensuring **parallel computation**.  

---

### 🎯 **Key Benefits of RDDs**  
✅ **Fault Tolerance** → Data is automatically recovered if a failure occurs 🔄  
✅ **Parallel Processing** → Speeds up computations across multiple machines 🚀  
✅ **Lazy Evaluation** → Optimizes execution by processing data only when needed 🏎️  
✅ **Immutability** → Ensures consistency by keeping original data unchanged 🔒  

---

## 🧑‍💻 **Decomposing RDDs in PySpark**

### What are Resilient Distributed Datasets (RDDs)? 🤔

An **RDD** is a fundamental data structure in **Spark**. Here's what RDD stands for:

* **Resilient**: Spark can handle failures and continue processing without any issues. It **recovers** data if something goes wrong. 💪
* **Distributed**: The data is **spread** across multiple machines or nodes, allowing Spark to handle large datasets efficiently. 🌍
* **Datasets**: An RDD is simply a **collection** of data that can be anything like arrays, tables, or tuples. 🗂️

In simple terms, an RDD is a **distributed collection** of data that Spark can process across multiple machines, while also being **fault-tolerant**.

---

## 🏗️ **Creating RDDs in PySpark**

You can create RDDs in PySpark from different sources. The two most common ways to create RDDs are:

### 1️⃣ **Parallelizing an Existing Collection**:

You can create RDDs by parallelizing an existing Python list or collection. This means that Spark will divide the list into smaller **partitions** and process them across multiple machines.

### 2️⃣ **External Datasets**:

You can create RDDs from **external datasets**, such as:

* **Files in HDFS (Hadoop Distributed File System)** 🗄️
* **Objects in an Amazon S3 bucket** ☁️
* **Lines in a text file** 📄

### 3️⃣ **From Existing RDDs**:

You can also create new RDDs by applying transformations to **existing RDDs**.

---

## 🔄 **Parallelizing Collections**

You can convert an existing Python collection (like a list) into an RDD using **parallelize()**. This function splits the collection into partitions and processes them in parallel.

### Example:

```python
# Parallelizing a list of numbers into an RDD
numRDD = sc.parallelize([1, 2, 3, 4])

# Parallelizing a string into an RDD
helloRDD = sc.parallelize("Hello world")

# Check the type of helloRDD
print(type(helloRDD))  # Output: <class 'pyspark.rdd.PipelinedRDD'>
```

The `helloRDD` is now a distributed collection (RDD) that Spark can process in parallel. ✨

---

## 📂 **From External Datasets**

Another way to create RDDs is by reading data from **external sources** such as a text file. You can use **textFile()** to load data from files and convert them into RDDs.

### Example:

```python
# Loading a file into an RDD
fileRDD = sc.textFile("README.md")

# Check the type of fileRDD
print(type(fileRDD))  # Output: <class 'pyspark.rdd.PipelinedRDD'>
```

Here, the file `README.md` is converted into an RDD, allowing Spark to process the file across multiple machines. 🌐

---

## 📊 **Understanding Partitioning in PySpark**

A **partition** is a logical division of a large dataset. Spark breaks down large datasets into smaller partitions so that it can process them in parallel across different machines or nodes.

### Example with **parallelize()**:

```python
# Creating an RDD with 6 partitions
numRDD = sc.parallelize(range(10), numSlices=6)
```

### Example with **textFile()**:

```python
# Loading a file with 6 partitions
fileRDD = sc.textFile("README.md", minPartitions=6)
```

You can check how many partitions an RDD has using the **getNumPartitions()** method:

```python
# Get the number of partitions in an RDD
numPartitions = numRDD.getNumPartitions()
print(numPartitions)
```

### Glomming Partitions:

You can also **glom** partitions to group them together and see the data inside each partition. This helps in debugging or understanding how data is distributed:

```python
# Glom to see data in each partition
rdd.glom()
```

---

## 🔍 **Checking File System in HDFS**

You can use the HDFS **fsck** command to check the **files**, **blocks**, and **locations** of data in HDFS:

```bash
hdfs fsck /user/talentum/stocks.csv -files -blocks -locations
```

This will give you details about the **location** and **health** of the file stored in HDFS. 📁

---

### 🧠 **Quick Recap**:

* **RDDs** are distributed collections of data that can be processed across machines and are **fault-tolerant**.
* You can create RDDs by **parallelizing** collections or loading **external datasets** like text files.
* **Partitioning** helps Spark process data in parallel, and you can check partition details using **getNumPartitions()**.

---

### 🔥 Overview of PySpark Operations  

![image](https://github.com/user-attachments/assets/ccff4a44-8a7c-4c61-9277-2ac240308f2a)  

PySpark, the Python API for Apache Spark, is all about handling large-scale data processing efficiently. It operates on two key concepts:  

#### 🐛 Transformations – Creating New RDDs  
Transformations are operations that take an RDD (Resilient Distributed Dataset) and create a new one without modifying the original. Think of it like a caterpillar turning into a butterfly—each transformation results in a new dataset.  

For example:  
```python
rdd1 = sparkContext.parallelize([1, 2, 3, 4])
rdd2 = rdd1.map(lambda x: x * 2)  # Transformation (map) creates a new RDD
```
Here, `map()` applies a function to each element, creating a new RDD (`rdd2`). The original RDD (`rdd1`) remains unchanged.  

#### 🖨️ Actions – Performing Computations on RDDs  
Actions trigger computations and return values. Until an action is performed, transformations are **lazy**, meaning they don’t execute immediately but wait for an action to trigger processing.  

For example:  
```python
result = rdd2.collect()  # Action (collect) triggers computation
print(result)  # Output: [2, 4, 6, 8]
```
Here, `collect()` gathers the elements of `rdd2` and prints them.  

So, remember:  
✅ **Transformations** create new RDDs but don’t execute immediately.  
✅ **Actions** trigger computation and return results.  

This way, PySpark optimizes processing by applying transformations lazily and executing only when needed! 🚀  

---

### ⚡ RDD Transformations – Lazy Evaluation  

![image](https://github.com/user-attachments/assets/d0be59c6-a464-4f04-a379-469a98b17b33)  

RDD transformations in PySpark are **lazy**, meaning they don’t execute immediately! Instead, they wait until an **action** is triggered, ensuring efficient computation by avoiding unnecessary processing.  

#### 🚀 How Lazy Evaluation Works  
Imagine a factory assembling a product but only running machines when an order is placed. Similarly, RDD transformations stack up, but PySpark waits until an action demands results before processing them.  

##### 🔗 Data Flow in Lazy Evaluation  
1️⃣ **RDD1** is created from storage (e.g., reading a file).  
2️⃣ Transformation applies → **RDD2** is generated but not processed yet.  
3️⃣ Another transformation applies → **RDD3** is ready but still waiting.  
4️⃣ Finally, an **action** executes → Computation occurs, and results are returned.  

#### 🔥 Basic RDD Transformations  
These fundamental operations help manipulate data efficiently:  

✅ `map()`: Applies a function to each element and returns a new RDD.  
```python
rdd = sparkContext.parallelize([1, 2, 3])
mapped_rdd = rdd.map(lambda x: x * 2)  # [2, 4, 6]
```  

✅ `filter()`: Extracts elements based on a condition.  
```python
filtered_rdd = rdd.filter(lambda x: x % 2 == 0)  # [2]
```  

✅ `flatMap()`: Flattens nested structures by splitting elements into multiple outputs.  
```python
rdd = sparkContext.parallelize(["Hello World"])
flat_mapped_rdd = rdd.flatMap(lambda x: x.split())  # ["Hello", "World"]
```  

✅ `union()`: Merges two RDDs into one.  
```python
rdd1 = sparkContext.parallelize([1, 2])
rdd2 = sparkContext.parallelize([3, 4])
union_rdd = rdd1.union(rdd2)  # [1, 2, 3, 4]
```  

### 📝 Recap:  
✨ **Transformations** create new RDDs but do not execute immediately.  
✨ **Lazy evaluation** optimizes performance by delaying computation.  
✨ Common transformations like `map()`, `filter()`, `flatMap()`, and `union()` help manipulate data efficiently.  

---

### 🔄 `map()` Transformation – Applying a Function to All Elements  

![image](https://github.com/user-attachments/assets/54629600-f45d-4bde-9ccb-61508c2d35c8)  

#### ✨ What is `map()` Transformation?  
The `map()` transformation is used in PySpark to apply a **function** to every element in an RDD, producing a **new RDD** with transformed values.  

Think of it like a **magic converter**—every item in the dataset passes through a function and comes out transformed!  

#### 🔍 Example Breakdown  
```python
RDD = sc.parallelize([1, 2, 3, 4])  # Creating an RDD with numbers  
RDD_map = RDD.map(lambda x: x * x)  # Squaring each number  
```
🔹 The `map()` function applies `lambda x: x * x` to each element in `RDD`.  
🔹 The new RDD (`RDD_map`) contains `[1, 4, 9, 16]`.  

#### 📊 Visual Representation  
Imagine the original RDD as a conveyor belt:  
**Before `map()` Transformation**: `[1, 2, 3, 4]`  
➡ Function applied (`x * x`)  
**After `map()` Transformation**: `[1, 4, 9, 16]`  

This transformation is **element-wise**, meaning it **processes each item independently**.  

#### 🚀 Key Points to Remember  
✅ `map()` **always returns a new RDD** (original RDD remains unchanged).  
✅ It is a **one-to-one transformation** (each input results in one output).  
✅ Used for **modifying values** (e.g., squaring, doubling, converting formats).  

---

### 🚦 `filter()` Transformation – Selecting Specific Elements  

![image](https://github.com/user-attachments/assets/6aa6dfaa-a6e2-4148-b552-69e55e2486b5)  

#### 🔍 What is `filter()` Transformation?  
The `filter()` transformation helps **extract only the elements that meet a specific condition**, creating a **new RDD** with the filtered results.  

Think of it like a **sieve**—it keeps what you need and removes the rest!  

#### ✨ Example Breakdown  
```python
RDD = sc.parallelize([1, 2, 3, 4])  # Creating an RDD with numbers  
RDD_filter = RDD.filter(lambda x: x > 2)  # Keep only numbers greater than 2  
```
🔹 The function `lambda x: x > 2` checks each element, keeping only `3` and `4`.  
🔹 The new RDD (`RDD_filter`) contains `[3, 4]`.  

#### 📊 Visual Representation  
Imagine the original RDD is a list of items:  
**Before `filter()` Transformation**: `[1, 2, 3, 4]`  
➡ Condition applied (`x > 2`)  
**After `filter()` Transformation**: `[3, 4]`  

### 🚀 Key Takeaways  
✅ `filter()` **creates a new RDD** with only selected elements.  
✅ It **removes** elements that don’t match the condition.  
✅ Used for **data preprocessing** (e.g., filtering errors, selecting relevant data).  


---

### 🌊 `flatMap()` Transformation – Expanding Elements  

![image](https://github.com/user-attachments/assets/4eebc285-9729-45f2-be1c-70eee10bc780)  

#### 🔍 What is `flatMap()` Transformation?  
Unlike `map()`, which transforms each element **one-to-one**, `flatMap()` **splits** elements and returns **multiple values** for each original item, creating a **flattened** RDD.  

Think of it like breaking sentences into individual words—each input expands into multiple outputs!  

#### ✨ Example Breakdown  
```python
RDD = sc.parallelize(["hello world", "how are you"])  
RDD_flatmap = RDD.flatMap(lambda x: x.split(" "))  
```
🔹 The function `lambda x: x.split(" ")` splits each string into words.  
🔹 The new RDD (`RDD_flatmap`) contains `["hello", "world", "how", "are", "you"]`.  

#### 📊 Visual Representation  
**Before `flatMap()` Transformation**:  
`["hello world", "how are you"]`  

➡ Function applied (`split()` on space)  

**After `flatMap()` Transformation**:  
`["hello", "world", "how", "are", "you"]`  

#### 🚀 Key Takeaways  
✅ `flatMap()` **splits elements into multiple outputs** (not one-to-one like `map()`).  
✅ Creates a **flattened RDD**, removing nested structures.  
✅ Useful for **text processing**, where sentences need to be broken into words.  



---

### 🔗 `union()` Transformation – Merging RDDs  

![image](https://github.com/user-attachments/assets/4bb17119-cc1a-4892-b5ca-cd9c3286b816)  

#### 🔍 What is `union()` Transformation?  
The `union()` transformation **combines two RDDs into a single RDD**, merging all elements while keeping duplicates.  

Think of it like **merging two lists**—you get everything from both, without any filtering!  

#### ✨ Example Breakdown  
```python
inputRDD = sc.textFile("logs.txt")  # Reading log file as RDD  

errorRDD = inputRDD.filter(lambda x: "error" in x.split())  # Filtering error messages  
warningsRDD = inputRDD.filter(lambda x: "warnings" in x.split())  # Filtering warnings  

combinedRDD = errorRDD.union(warningsRDD)  # Merging both RDDs  
```
🔹 `errorRDD` keeps lines containing **"error"**  
🔹 `warningsRDD` keeps lines containing **"warnings"**  
🔹 `union()` merges both, keeping all elements  

#### 📊 Visual Representation  
Imagine two lists:  
**Before `union()` Transformation**  
`errorRDD`: `["Error: Disk Full", "Error: Timeout"]`  
`warningsRDD`: `["Warning: Low Memory", "Warning: High CPU Usage"]`  

➡ `union()` merges them  

**After `union()` Transformation**  
`["Error: Disk Full", "Error: Timeout", "Warning: Low Memory", "Warning: High CPU Usage"]`  

#### 🚀 Key Takeaways  
✅ `union()` **combines two RDDs** while keeping duplicates  
✅ Useful for **merging filtered results** (like logs, events, data subsets)  
✅ Doesn’t remove duplicates—both datasets are preserved  

---

## ⚡ **RDD Actions in PySpark**

### What are RDD Actions? 🤔

**Actions** are operations that **trigger a computation** and return a value after running the computation on the RDD. They are the final step that brings the results of RDD transformations to the **driver** program. 🏁

Common **Basic RDD Actions** include:

* **collect()**: Brings all elements of the dataset to the driver program as a list. 📜
* **take(N)**: Returns the first **N** elements of the dataset. 🔢
* **first()**: Returns the **first element** of the dataset. 🔑
* **count()**: Returns the **number of elements** in the RDD. 📊

---

## 📦 **Understanding collect() and take() Actions**

### 1️⃣ **collect()** Action:

The **collect()** action gathers all the elements from the RDD and brings them to the **driver** program as a Python **list**.

#### Example:

```python
RDD_map = sc.parallelize([1, 2, 3, 4])
squaredRDD = RDD_map.map(lambda x: x ** 2)

# Collect all the elements of the RDD
print(squaredRDD.collect())  
# Output: [1, 4, 9, 16]
```

### 2️⃣ **take(N)** Action:

The **take(N)** action returns the first **N** elements of the dataset as a list.

#### Example:

```python
RDD_map = sc.parallelize([1, 2, 3, 4])

# Take the first 2 elements of the RDD
print(RDD_map.take(2))  
# Output: [1, 2]
```

---

## 🧑‍💻 **first() and count() Actions**

### 1️⃣ **first()** Action:

The **first()** action returns the **first element** of the RDD.

#### Example:

```python
RDD_map = sc.parallelize([1, 2, 3, 4])

# Get the first element
print(RDD_map.first())  
# Output: 1
```

### 2️⃣ **count()** Action:

The **count()** action returns the **number of elements** in the RDD.

#### Example:

```python
RDD_flatmap = sc.parallelize([1, 2, 3, 4, 5])

# Count the number of elements
print(RDD_flatmap.count())  
# Output: 5
```

---

## 🧪 **Lab Example: Using Actions with RDDs**

Here’s an example demonstrating how to use the **map()** transformation and **RDD actions**.

### Step 1: Cube Numbers in an RDD

```python
# Create an RDD from a list of numbers
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbRDD = sc.parallelize(numbers)

# Cube the numbers using map() transformation
cubedRDD = numbRDD.map(lambda x: x ** 3)

# Collect the results (get the entire dataset)
numbers_all = cubedRDD.collect()

# Print the cubed numbers
for numb in numbers_all:
    print(numb)
```

#### Output:

```
1
8
27
64
125
216
343
512
729
1000
```

---

### Step 2: Filter Lines Containing the Keyword "Spark" in a File

```python
file_path = 'file:////home/talentum/spark/README.md'

# Load the file into an RDD
fileRDD = sc.textFile(file_path)

# Filter the fileRDD for lines that contain the word "Spark"
fileRDD_filter = fileRDD.filter(lambda line: 'Spark' in line)

# Count the number of lines containing the word "Spark"
print("The total number of lines with the keyword Spark is", fileRDD_filter.count())

# Print the first 4 lines containing the word "Spark"
for line in fileRDD_filter.take(4):
    print(line)
```

#### Output:

```
The total number of lines with the keyword Spark is 19
# Apache Spark
Spark is a fast and general cluster computing system for Big Data. It provides
rich set of higher-level tools including Spark SQL for SQL and DataFrames,
and Spark Streaming for stream processing.
```

---

## 📚 **Quick Recap**:

* **RDD Actions** trigger the computation and bring results to the driver program.
* **collect()** retrieves all elements as a list, while **take(N)** returns the first **N** elements.
* **first()** returns the first element, and **count()** returns the number of elements in the RDD.

With these actions, you can efficiently retrieve, filter, and count data within RDDs! 🎉

---

## 🔑 **Introduction to Pair RDDs in PySpark**

In real-life datasets, the data is often structured as **key-value pairs**, where each row is a **key** that maps to one or more **values**.

* **Pair RDD** is a special kind of RDD that allows you to work with key-value pairs.
* **Key** is the identifier (e.g., an ID or name) and **value** is the data associated with that key.

This makes it easy to perform operations like grouping, sorting, or combining data based on the key. 🔄

---

## 🛠️ **Creating Pair RDDs**

### 1️⃣ **From a List of Key-Value Tuples**

You can create a pair RDD by directly passing a list of tuples, where each tuple contains a key and a value.

#### Example:

```python
my_tuple = [('Sam', 23), ('Mary', 34), ('Peter', 25)] 
pairRDD_tuple = sc.parallelize(my_tuple)
```

### 2️⃣ **From a Regular RDD**

You can also convert a regular RDD into a pair RDD by using **map()** and splitting the data into key-value pairs.

#### Example:

```python
my_list = ['Sam 23', 'Mary 34', 'Peter 25'] 
regularRDD = sc.parallelize(my_list)

# Convert the regular RDD to a pair RDD
pairRDD_RDD = regularRDD.map(lambda s: (s.split(' ')[0], s.split(' ')[1]))
```

---

## 🔄 **Transformations on Pair RDDs**

Just like regular RDDs, **pair RDDs** support many transformations. However, you need to pass functions that operate on **key-value pairs**, not individual elements.

Some common pair RDD transformations include:

* **reduceByKey(func)**: Combine values with the same key.
* **groupByKey()**: Group values with the same key.
* **sortByKey()**: Sort the RDD by key.
* **join()**: Join two pair RDDs based on their key.

---

## ➗ **reduceByKey() Transformation**

The **reduceByKey()** transformation combines the values associated with the same key. It runs in parallel across the dataset, performing the operation on each key.

#### Example:

```python
regularRDD = sc.parallelize([("Messi", 23), ("Ronaldo", 34), ("Neymar", 22), ("Messi", 24)])

# Combine values with the same key
pairRDD_reducebykey = regularRDD.reduceByKey(lambda x, y: x + y)

# Collect the results
print(pairRDD_reducebykey.collect())
# Output: [('Neymar', 22), ('Ronaldo', 34), ('Messi', 47)]
```

---

## 🔢 **sortByKey() Transformation**

The **sortByKey()** operation sorts the pair RDD by its key, either in ascending or descending order.

#### Example:

```python
pairRDD_reducebykey_rev = pairRDD_reducebykey.map(lambda x: (x[1], x[0]))

# Sort by key in descending order
sorted_RDD = pairRDD_reducebykey_rev.sortByKey(ascending=False)

# Collect the results
print(sorted_RDD.collect())
# Output: [(47, 'Messi'), (34, 'Ronaldo'), (22, 'Neymar')]
```

---

## 🔀 **groupByKey() Transformation**

The **groupByKey()** transformation groups all values with the same key together in the pair RDD.

#### Example:

```python
airports = [("US", "JFK"), ("UK", "LHR"), ("FR", "CDG"), ("US", "SFO")]
regularRDD = sc.parallelize(airports)

# Group values with the same key
pairRDD_group = regularRDD.groupByKey().collect()

# Print the results
for cont, air in pairRDD_group:
    print(cont, list(air))
# Output:
# FR ['CDG']
# US ['JFK', 'SFO']
# UK ['LHR']
```

---

## 🔗 **join() Transformation**

The **join()** transformation allows you to join two pair RDDs based on their keys. It returns a new RDD containing the joined data.

#### Example:

```python
RDD1 = sc.parallelize([("Messi", 34), ("Ronaldo", 32), ("Neymar", 24)])
RDD2 = sc.parallelize([("Ronaldo", 80), ("Neymar", 120), ("Messi", 100)])

# Join the two RDDs based on their key (name)
joined_RDD = RDD1.join(RDD2)

# Collect the results
print(joined_RDD.collect())
# Output: [('Neymar', (24, 120)), ('Ronaldo', (32, 80)), ('Messi', (34, 100))]
```

---

## 📚 **Quick Recap**:

* **Pair RDDs** are special RDDs that allow you to work with **key-value pairs**.
* You can create pair RDDs from **lists of tuples** or **regular RDDs** by using **map()**.
* Common transformations include **reduceByKey()**, **groupByKey()**, **sortByKey()**, and **join()**.
* These transformations enable powerful operations like **grouping**, **sorting**, and **combining data** based on keys. 🎉

With pair RDDs, you can easily process key-value datasets like user data, logs, etc.! 🚀

---

# 🚀 **PySpark Actions: Transforming and Aggregating RDDs**  

Actions in PySpark trigger computation and return results to the driver program. Unlike transformations, actions **execute immediately** and generate **final outputs**. Let’s simplify these concepts with examples! 😊  

---

## 🔹 **reduce() Action**  

✅ **Aggregates elements in an RDD using a specified function**.  
✅ The function must be **commutative** (order does not change the result) and **associative** (grouping does not affect the result).  

📜 **Example of reduce() in PySpark:**  
```python
x = [1, 3, 4, 6]  
RDD = sc.parallelize(x)  
RDD.reduce(lambda x, y: x + y)  # Output: 14
```
💡 **Think of `reduce()` like summing up values in a shopping cart**—it combines all elements efficiently!  

---

## 📝 **saveAsTextFile() Action**  

✅ Saves an RDD **into a text file inside a directory**, with **each partition stored as a separate file**.  
✅ Use `coalesce()` to **combine partitions** and save the RDD as **a single text file**.  

📜 **Example Usage:**  
```python
RDD.saveAsTextFile("tempFile")  # Saves data into multiple files  
RDD.coalesce(1).saveAsTextFile("tempFile")  # Saves as a single file  
```
🚀 **This is a transformation operation, still generating a new RDD!**  

💡 **Imagine exporting a dataset—by default, PySpark saves multiple files, but `coalesce(1)` combines everything into a single file for easier management!**  

---

## 🔄 **Action Operations on Pair RDDs**  

✅ **Pair RDDs store key-value data**, allowing easy aggregation and retrieval.  
✅ Common actions used in **pair RDDs** include:  
   - `countByKey()`
   - `collectAsMap()`  

📜 **Example of `countByKey()` on a simple list:**  
```python
rdd = sc.parallelize([("a", 1), ("b", 1), ("a", 1)])  
for key, val in rdd.countByKey().items():  
    print(key, val)  
# Output:
# 'a' → 2
# 'b' → 1
```
🚀 **This counts occurrences of each key efficiently!**  

---

## 🔍 **collectAsMap() Action**  

✅ **Converts an RDD into a dictionary**, preserving **key-value pairs**.  
✅ **Efficiently retrieves all values** without needing iterative lookups.  

📜 **Example Usage:**  
```python
sc.parallelize([(1, 2), (3, 4)]).collectAsMap()
# Output: {1: 2, 3: 4}
```
💡 **Think of this like converting a list into a quick-access dictionary!** 🔥  

---

### 🎯 **Key Takeaways:**  
✅ **`reduce()` aggregates elements efficiently.**  
✅ **`saveAsTextFile()` writes RDDs to files, with `coalesce()` ensuring a single output file.**  
✅ **Pair RDD actions leverage key-value operations for easy aggregation (`countByKey()`, `collectAsMap()`).**  
✅ **Actions return final results, while transformations create new RDDs.**  

---

# 🏗️ **Lab: Action Operations in PySpark RDDs**  

This lab explores **RDD actions** such as `countByKey()` and `flatMap()` in PySpark, demonstrating their ability to **process data and return results** efficiently. Let’s break it down step by step! 😊  

---

## 🔹 **Counting Keys in an RDD**  

✅ Uses `countByKey()` to **count occurrences of each key** in a pair RDD.  
✅ Returns a **default dictionary**, storing counts for each unique key.  
✅ `countByKey()` is an **action**, meaning it triggers computation **immediately** and **does not create a new RDD**.  

📜 **Example Code:**  
```python
dataset = [(1, 2), (3, 4), (3, 6), (4, 5)]
Rdd = sc.parallelize(dataset)

# Apply countByKey action
total = Rdd.countByKey()

# Check the type
print("The type of total is", type(total))

# Iterate over the result
for k, v in total.items(): 
  print("key", k, "has", v, "counts")
```
📌 **Expected Output:**  
```
The type of total is <class 'collections.defaultdict'>
key 1 has 1 counts
key 3 has 2 counts
key 4 has 1 counts
```
🚀 **This confirms `countByKey()` returns key counts as a `defaultdict` instead of a new RDD!**  

---

## 🏷️ **Reading and Processing a Text File**  

✅ **Creates an RDD from a text file**, ensuring the file exists before reading.  
✅ **Uses `flatMap()` to split lines into individual words**, expanding each line into multiple elements.  
✅ Applies `.count()` to **compute the total number of words in the dataset**.  

📜 **Example Code:**  
```python
file_path = "file:///home/talentum/test-jupyter/P2/M2/SM4/4_AdvancedRddActions/Dataset/Complete_Shakespeare.txt"

# Create RDD from file
baseRDD = sc.textFile(file_path)

# Split lines into words
splitRDD = baseRDD.flatMap(lambda x: x.split())

# Count total words
print("Total number of words in splitRDD:", splitRDD.count())
```
📌 **Expected Output:**  
```
Total number of words in splitRDD: 128576
```
💡 **This demonstrates how to efficiently process a large text file using RDD actions!**  

---

### 🎯 **Key Takeaways:**  
✅ **`countByKey()` counts occurrences of each key, returning a dictionary.**  
✅ **Actions trigger computation immediately, unlike transformations.**  
✅ **Reading a text file with `textFile()` and splitting data using `flatMap()` allows efficient processing.**  
✅ **PySpark is optimized for handling large-scale datasets dynamically.**  

---

# 📌 **Text Processing in PySpark: Word Frequency Analysis**  

This lab explores **RDD transformations and actions** using PySpark to **process and analyze text data** from the *Complete Works of Shakespeare*. Let’s break down each step! 😊  

---

## 🏗️ **Step 1: Reading and Preprocessing the Text File**  

✅ **Load the dataset** using `sc.textFile()` to create an RDD from a file.  
✅ **Split the text** into individual words using `flatMap()`.  
✅ **Convert words to lowercase** and **remove stop words** using `filter()`.  

📜 **Code Example:**  
```python
file_path = "file:///home/talentum/test-jupyter/P2/M2/SM4/4_AdvancedRddActions/Dataset/Complete_Shakespeare.txt"

# Create a baseRDD from the file path
baseRDD = sc.textFile(file_path)

# Split lines into words
splitRDD = baseRDD.flatMap(lambda x: x.split(' '))

# Convert words to lowercase and remove stop words
splitRDD_no_stop = splitRDD.filter(lambda x: x.lower() not in stop_words)
```
💡 **This step ensures we only process meaningful words without common stop words!**  

---

## 🔍 **Step 2: Word Count Computation**  

✅ **Create key-value pairs** (`(word, 1)`) using `map()`.  
✅ **Use `reduceByKey()` to count occurrences** of each unique word in the dataset.  

📜 **Code Example:**  
```python
# Create (word, 1) tuples
splitRDD_no_stop_words = splitRDD_no_stop.map(lambda w: (w.lower(), 1))

# Count occurrences of each word
resultRDD = splitRDD_no_stop_words.reduceByKey(lambda x, y: x + y)

# Display some results
print(resultRDD.take(10))
```
📌 **Expected Output:**  
```
[('project', 40), ('gutenberg', 35), ('ebook', 4), ('complete', 33), ('works', 35), ('william', 39), ('shakespeare,', 1), ('shakespeare', 42), ('', 65498), ('use', 68)]
```
💡 **This helps analyze word frequencies efficiently in large-scale text data!** 🚀  

---

## 📊 **Step 3: Sorting Word Frequencies**  

✅ **Swap keys and values** (`(count, word)`) to enable sorting by frequency.  
✅ **Use `sortByKey(False)` to arrange words in descending order** of occurrence.  
✅ **Retrieve the top 10 most frequently used words**.  

📜 **Code Example:**  
```python
# Swap (word, count) → (count, word)
resultRDD_swap = resultRDD.map(lambda x: (x[1], x[0]))

# Sort by count in descending order
resultRDD_swap_sort = resultRDD_swap.sortByKey(ascending=False)

# Display the top 10 most frequent words
for word in resultRDD_swap_sort.take(10):
    print("{} has {} counts".format(word[1], word[0]))
```
📌 **Expected Output:**  
```
thou has 650 counts
thy has 574 counts
shall has 393 counts
would has 311 counts
good has 295 counts
thee has 286 counts
love has 273 counts
Enter has 269 counts
th' has 254 counts
```
💡 **This confirms common Shakespearean words like "thou" and "thy" appear frequently!** 🔥  

---

### 🎯 **Key Takeaways:**  
✅ **PySpark efficiently processes massive text files** with distributed computing.  
✅ **Actions like `reduceByKey()` compute word frequencies efficiently**.  
✅ **Sorting allows quick identification of the most used words**.  
✅ **Using `filter()` removes unnecessary stop words**, keeping only meaningful data.  

---

# 🏗️ **Performing RDD Operations on `constitution.txt`**  

This lab demonstrates **how to process, count, and sort word occurrences** in a dataset using **PySpark RDD transformations and actions**. Let’s break it down step by step! 😊  

---

## 🔍 **Step 1: Read and Preprocess the Text File**  

✅ **Load the text file** into an RDD using `sc.textFile()`.  
✅ **Split the lines** into individual words using `flatMap()`.  
✅ **Create key-value pairs** (`(word, 1)`) using `map()`.  
✅ **Aggregate occurrences** of each word using `reduceByKey()`.  

📜 **Example Code:**  
```python
# Read the file from HDFS
rdd_lines = sc.textFile("constitution.txt")

# Tokenize words
rdd_words = rdd_lines.flatMap(lambda line: line.split())

# Convert words into key-value pairs
rdd_tup = rdd_words.map(lambda word: (word, 1))

# Aggregate word counts
rdd_final = rdd_tup.reduceByKey(lambda x, y: x + y)

# Display top word counts
print(rdd_final.take(7))
```
📌 **Expected Output:**  
```
[('We', 2), ('the', 662), ('People', 2), ('of', 493), ('United', 85), ('States,', 55), ('in', 137)]
```
🚀 **This confirms `reduceByKey()` efficiently aggregates word occurrences!**  

---

## 🔄 **Step 2: Sorting Words by Frequency**  

✅ **Swap key-value pairs** (`(count, word)`) for sorting purposes.  
✅ **Use `sortByKey(False)` to order words by highest frequency first**.  
✅ **Retrieve the top 7 most frequently used words**.  

📜 **Example Code:**  
```python
# Swap (word, count) → (count, word)
rdd_swap = rdd_final.map(lambda tup: (tup[1], tup[0]))

# Sort words by count in descending order
rdd_sorted = rdd_swap.sortByKey(ascending=False)

# Display top words
print(rdd_sorted.take(7))
```
📌 **Expected Output:**  
```
[(662, 'the'), (493, 'of'), (293, 'shall'), (256, 'and'), (183, 'to'), (178, 'be'), (157, 'or')]
```
💡 **This step ranks the most frequent words from the Constitution efficiently!**  

---

## 🏎️ **Step 3: One-Liner Implementation**  

💡 If you prefer a **single-line command**, you can simplify the process:  
```python
print(sc.textFile("constitution.txt").flatMap(lambda line: line.split()).map(lambda word: (word, 1)).reduceByKey(lambda x, y: x + y).map(lambda tup: (tup[1], tup[0])).sortByKey(ascending=False).take(7))
```
📌 **Expected Output:**  
```
[(662, 'the'), (493, 'of'), (293, 'shall'), (256, 'and'), (183, 'to'), (178, 'be'), (157, 'or')]
```
🚀 **This one-liner performs the entire workflow efficiently!**  

---

### 🎯 **Key Takeaways:**  
✅ **RDD actions like `reduceByKey()` efficiently count word occurrences**.  
✅ **Swapping key-value pairs allows sorting by frequency (`sortByKey(False)`)**.  
✅ **One-liner implementations streamline complex operations**.  

---

# 🚀 **PySpark: Verbosity & Data Pipeline as USPs**  

PySpark is known for its **verbosity**, meaning it provides detailed logs and error messages to aid debugging. Additionally, its **data pipeline capabilities** allow for efficient processing of distributed datasets. These features make PySpark a **preferred choice** for **big data transformations**. 😊  

---

## 🏗️ **Standalone vs. Jupyter Notebook in PySpark**  

✅ **Standalone applications** require creating a **separate file** and running it.  
✅ **Jupyter Notebook is not standalone**—it is designed for **interactive development and testing**.  
✅ **Jupyter is ideal for exploratory analysis**, but **not typically used in production**.  

💡 **Think of Jupyter like a sandbox**—you test and refine your code before deploying it in production using **standalone applications**! 🚀  

---

# 🔥 **Running PySpark via `spark-submit`**
### 🛠 **Setting Up a Standalone PySpark Script**
✅ **Python Path Check:**  
```sh
which python  
/usr/bin/python  
```
✅ **Create a Python file (`wordcount.py`)**  
✅ **Ensure Spark is used instead of the Python shell (`spark-submit`)**  

📜 **Running the script:**  
```sh
spark-submit wordcount.py  
```

### ❗ **Common Errors & Fixes**
🚀 **Issue:** `"Jupyter not found"`  
✅ **Fix:** Run →  
```sh
source /home/talentum/shared/unset_jupyter.sh  
```
🚀 **Issue:** `"name 'sc' is not defined"`  
✅ **Fix:** Add the following after the shebang (`#!`):  
```python
# Entrypoint for Spark (2.x+)
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("Spark SQL basic example").enableHiveSupport().getOrCreate()
sc = spark.sparkContext
```
🚀 **Issue:** Running with YARN  
✅ **Fix:** Specify the `.master("yarn")`  
```python
spark = SparkSession.builder.appName("Spark SQL basic example").enableHiveSupport().master("yarn").getOrCreate()
```

📜 **Final Execution:**  
```sh
spark-submit wordcount.py
echo $?
0  # Execution successful!
```

![image](https://github.com/user-attachments/assets/75daa605-d8dd-4729-97f8-4da2d286f1bd)

---

### 🎯 **Key Takeaways**
✅ **PySpark is verbose, providing helpful logs for debugging.**  
✅ **Standalone applications require `spark-submit`, unlike Jupyter.**  
✅ **RDD processing optimizes text parsing & word frequency analysis.**  
✅ **Sorting allows quick identification of commonly used words.**  
✅ **Setting up `SparkSession` resolves environment issues.**

---

# 🚀 **PySpark SQL & DataFrames**  

## 🔹 **Introduction to PySpark DataFrames**  
PySparkSQL is a **library for structured data processing** that provides insights into **data structure and computation**.  

✅ **DataFrame is an immutable distributed collection of data with named columns**.  
✅ Designed for **structured (RDBMS) and semi-structured (JSON) data processing**.  
✅ **Supports SQL queries (`SELECT * FROM table`)** and **expression methods (`df.select()`)**.  
✅ DataFrame API is available in **Python, R, Scala, and Java**.  

💡 **Think of PySpark DataFrames as an enhanced version of Pandas DataFrames but optimized for big data and distributed computing!** 🚀  

---

## 🏗️ **SparkSession: Entry Point for DataFrame API**  

✅ **SparkContext is the main entry point for creating RDDs**, but for DataFrames, you use **SparkSession**.  
✅ **SparkSession provides a unified entry point** to manage DataFrames and execute SQL queries.  
✅ Available in **PySpark shell as `spark`**.  

📜 **Example:**  
```python
from pyspark.sql import SparkSession

# Create a Spark session
spark = SparkSession.builder.appName("PySpark SQL Example").getOrCreate()
```
🚀 **This allows direct interaction with Spark's SQL API and DataFrame operations!**  

---

## 🔄 **Creating DataFrames in PySpark**  

PySpark supports **two primary ways** to create DataFrames:  

1️⃣ **From existing RDDs** using `createDataFrame()`  
```python
rdd = spark.sparkContext.parallelize([(1, "Alice"), (2, "Bob")])
df = spark.createDataFrame(rdd, ["ID", "Name"])
df.show()
```  

2️⃣ **From data sources (CSV, JSON, TXT)** using `spark.read`  
```python
df_csv = spark.read.csv("data.csv", header=True, inferSchema=True)
df_csv.show()
```  

✅ **Schema helps optimize queries** by providing metadata (column names, data types, missing values).  
✅ **RDDs do not have schemas, but DataFrames contain both schema and data** for structured processing.  

💡 **Think of schema as a blueprint for your data**—it ensures consistency and enhances query performance!  

---

### 🎯 **Key Takeaways**  
✅ PySparkSQL processes **structured & semi-structured data** efficiently.  
✅ **SparkSession is the entry point** for DataFrames and SQL queries.  
✅ **DataFrames support SQL-like queries (`SELECT * FROM table`) and API methods (`df.select()`).**  
✅ **Schemas improve data handling**, unlike RDDs which lack structured metadata.  

---

# 🚀 **Creating DataFrames in PySpark**  

DataFrames in PySpark are **structured and optimized** for efficient data processing, unlike RDDs which lack schema definitions. Here’s how you can create **DataFrames from RDDs and external files**. 😊  

---

## 🔹 **Create a DataFrame from an RDD**  

✅ **Convert an RDD into a DataFrame** using `createDataFrame()`.  
✅ **Provide schema (column names) to structure the data**.  

📜 **Example Code:**  
```python
iphones_RDD = sc.parallelize([
    ("XS", 2018, 5.65, 2.79, 6.24),
    ("XR", 2018, 5.94, 2.98, 6.84),
    ("X10", 2017, 5.65, 2.79, 6.13),
    ("8Plus", 2017, 6.23, 3.07, 7.12)
])

# Define schema
names = ['Model', 'Year', 'Height', 'Width', 'Weight']

# Convert RDD to DataFrame
iphones_df = spark.createDataFrame(iphones_RDD, schema=names)

# Verify DataFrame type
print(type(iphones_df))
```
📌 **Expected Output:**  
```
<class 'pyspark.sql.dataframe.DataFrame'>
```
🚀 **This ensures structured data processing with named columns!**  

---

## 🏗️ **Create a DataFrame from CSV/JSON/TXT**  

✅ **Use `spark.read` to load structured files** (CSV, JSON, TXT).  
✅ **Specify `header=True` to use the first row as column names**.  
✅ **Use `inferSchema=True` to automatically detect column types**.  

📜 **Example Code:**  
```python
# Load CSV file
df_csv = spark.read.csv("people.csv", header=True, inferSchema=True)

# Load JSON file
df_json = spark.read.json("people.json", header=True, inferSchema=True)

# Load TXT file
df_txt = spark.read.text("people.txt")
```
💡 **Key Parameters:**  
✅ **`header=True`** → Uses the first row as headers.  
✅ **`inferSchema=True`** → Detects column data types automatically.  

---

### 🎯 **Key Takeaways**  
✅ **DataFrames provide structured processing**, unlike RDDs.  
✅ **Schema improves readability and query optimization**.  
✅ **Use `spark.read` to load CSV, JSON, and TXT files efficiently**.  
✅ **Apply `header=True, inferSchema=True` to auto-define column names & types**.  

---

# 🏗️ **PySpark Lab: Creating & Managing DataFrames**  

This lab explores **creating DataFrames in PySpark** from an **RDD and a CSV file**, checking schema structure, and verifying data types. Let's break it down step by step! 😊  

---

## 🔹 **Create a DataFrame from an RDD**  

✅ **Convert an RDD into a DataFrame** using `createDataFrame()`.  
✅ **Define a schema (`Name`, `Age`) to structure the DataFrame**.  

📜 **Example Code:**  
```python
# Create a list of tuples
sample_list = [('Mona', 20), ('Jennifer', 34), ('John', 20), ('Jim', 26)]

# Create an RDD from the list
rdd = sc.parallelize(sample_list)

# Convert RDD into a DataFrame with a schema
names_df = spark.createDataFrame(rdd, schema=['Name', 'Age'])

# Check the DataFrame type
print("The type of names_df is", type(names_df))
```
📌 **Expected Output:**  
```
The type of names_df is <class 'pyspark.sql.dataframe.DataFrame'>
```
💡 **This confirms a structured DataFrame with named columns!** 🚀  

---

## 🏗️ **Create a DataFrame from a CSV File**  

✅ **Load structured data from a file using `spark.read.csv()`**.  
✅ **Apply schema detection with `header=True, inferSchema=True`**.  
✅ **Check schema details using `.schema`**.  

📜 **Example Code:**  
```python
file_path = "file:///home/talentum/shared/6_Spark/data/1_AbstractingDatawithDataFrames/Dataset/people.csv"

# Load DataFrame from CSV file
people_df = spark.read.csv(file_path, header=True, inferSchema=True)

# Check the DataFrame type
print("The type of people_df is", type(people_df))

# Display a sample of the DataFrame
people_df.show()

# Print the schema of the DataFrame
print(people_df.schema)
```
📌 **Expected Output (Schema Format):**  
```
StructType(List(
    StructField(_c0,IntegerType,true),
    StructField(person_id,IntegerType,true),
    StructField(name,StringType,true),
    StructField(sex,StringType,true),
    StructField(date of birth,StringType,true)
))
```
💡 **PySpark DataFrames require an associated schema, ensuring optimized queries & structured data processing!**  

---

### 🎯 **Key Takeaways:**  
✅ **DataFrames can be created from RDDs using `createDataFrame()`**.  
✅ **`spark.read.csv()` loads structured files efficiently**.  
✅ **`header=True` uses the first row for column names**.  
✅ **`inferSchema=True` automatically detects data types**.  
✅ **A DataFrame **must have a schema**, unlike raw RDDs.  

---

# 🚀 **PySpark DataFrame Operators: Transformations & Actions**  

PySpark **DataFrame operations** can be divided into two categories:  
✅ **Transformations** → Modify or filter DataFrames without executing immediately.  
✅ **Actions** → Execute and return results to the driver program.  

---

## 🔹 **Common DataFrame Transformations**  
- `select()` → Subset specific columns.  
- `filter()` → Filter rows based on conditions.  
- `groupBy()` → Group data based on a column.  
- `orderBy()` → Sort DataFrame rows.  
- `dropDuplicates()` → Remove duplicate records.  
- `withColumnRenamed()` → Rename columns for better readability.  

## 🔹 **Common DataFrame Actions**  
- `printSchema()` → Display DataFrame schema.  
- `head()` → Retrieve the first row.  
- `show()` → Display the first 20 rows (default).  
- `count()` → Return total number of rows.  
- `columns` → List DataFrame column names.  
- `describe()` → Summarize DataFrame statistics.  

---

## 🏗️ **select() & show() Operations**  

✅ **`select()` extracts specific columns**.  
✅ **`show()` prints the first 20 rows (default) in tabular format**.  

📜 **Example Usage:**  
```python
df_id_age = test.select("Age")  
df_id_age.show(3)
```
📌 **Expected Output:**  
```
+---+
|Age|
+---+
| 17|
| 17|
| 17|
+---+
only showing top 3 rows
```
💡 **This allows efficient column selection while maintaining structured output!**  

---

## 🔍 **filter() & show() Operations**  

✅ **`filter()` removes rows based on a condition**.  
✅ **`show()` displays the filtered results**.  

📜 **Example Usage:**  
```python
new_df_age21 = new_df.filter(new_df.Age > 21)  
new_df_age21.show(3)
```
📌 **Expected Output:**  
```
+-------+------+---+
|User_ID|Gender|Age|
+-------+------+---+
|1000002|    M| 55|
|1000003|    M| 26|
|1000004|    M| 46|
+-------+------+---+
only showing top 3 rows
```
🚀 **This efficiently filters data while keeping the structure intact!**  

---

## 🔄 **groupBy() & count() Operations**  

✅ **`groupBy()` groups DataFrame rows based on a column**.  
✅ **`count()` returns the total count per group**.  

📜 **Example Usage:**  
```python
test_df_age_group = test_df.groupby("Age")  
test_df_age_group.count().show(3)
```
📌 **Expected Output:**  
```
+---+------+
|Age| count|
+---+------+
| 26|219587|
| 17|     4|
| 55| 21504|
+---+------+
only showing top 3 rows
```
💡 **This is an action, not a transformation—it triggers computation immediately!**  

---

### 🎯 **Key Takeaways:**  
✅ **Transformations modify the DataFrame but don’t execute immediately**.  
✅ **Actions compute results and return them to the driver program**.  
✅ **`select()`, `filter()`, `groupBy()`, and `show()` allow efficient data exploration**.  
✅ **Grouping and counting enables better analysis of categorical data**.  

---

# 🚀 **PySpark DataFrame Transformations & Actions**  

DataFrames in PySpark support **various operations** that help in data transformation and analysis. Let's break down the **key transformations and actions** with clear explanations and examples! 😊  

---

## 🔄 **DataFrame Transformations**  
Transformations modify a DataFrame but **do not execute immediately**.  
They are applied **lazily** and require an action to trigger computation.

### 🔹 **`orderBy()` Transformation**
✅ **Sorts the DataFrame based on one or more columns**.  

📜 **Example Usage:**  
```python
test_df_age_group.count().orderBy("Age").show(3)
```
📌 **Expected Output:**  
```
+---+-----+
|Age|count|
+---+-----+
|  0|15098|
| 17|    4|
| 18|99660|
+---+-----+
only showing top 3 rows
```
💡 **`orderBy()` ensures rows are sorted efficiently** for better readability and analysis!  

---

### 🔹 **`dropDuplicates()` Transformation**  
✅ **Removes duplicate rows from a DataFrame**.  

📜 **Example Usage:**  
```python
test_df_no_dup = test_df.select("User_ID", "Gender", "Age").dropDuplicates()
print(test_df_no_dup.count())
```
📌 **Expected Output:**  
```
5892
```
🚀 **Ideal for cleaning datasets while retaining only unique records!**  

---

### 🔹 **`withColumnRenamed()` Transformation**  
✅ **Renames a specific column in the DataFrame**.  

📜 **Example Usage:**  
```python
test_df_sex = test_df.withColumnRenamed("Gender", "Sex")
test_df_sex.show(3)
```
📌 **Expected Output:**  
```
+-------+---+---+
|User_ID|Sex|Age|
+-------+---+---+
|1000001|  F| 17|
|1000001|  F| 17|
|1000001|  F| 17|
+-------+---+---+
```
💡 **Useful when renaming column names for better clarity in analysis!**  

---

## ⚡ **DataFrame Actions**  
Actions **trigger computation** and return results to the driver program.

### 🔹 **`printSchema()` Action**  
✅ **Displays column types in the DataFrame schema**.  

📜 **Example Usage:**  
```python
test_df.printSchema()
```
📌 **Expected Output:**  
```
|-- User_ID: integer (nullable = true)
|-- Product_ID: string (nullable = true)
|-- Gender: string (nullable = true)
|-- Age: string (nullable = true)
|-- Occupation: integer (nullable = true)
|-- Purchase: integer (nullable = true)
```
🚀 **Helps verify data structure before performing transformations!**  

---

### 🔹 **`columns` Action**  
✅ **Lists all column names in the DataFrame**.  

📜 **Example Usage:**  
```python
print(test_df.columns)
```
📌 **Expected Output:**  
```
['User_ID', 'Gender', 'Age']
```
💡 **Useful for checking available fields in the DataFrame!**  

---

### 🔹 **`describe()` Action**  
✅ **Computes summary statistics for numerical columns**.  
✅ **Can help detect outliers in the dataset**.  

📜 **Example Usage:**  
```python
test_df.describe().show()
```
📌 **Expected Output:**  
```
+-------+------------------+------+------------------+
|summary| User_ID | Gender | Age |
+-------+------------------+------+------------------+
| count | 550068 | 550068 | 550068 |
| mean  | 1003028.8424013031 | null | 30.38 |
| stddev| 1727.5915855307312 | null | 11.86 |
| min   | 1000001 | F | 0 |
| max   | 1006040 | M | 55 |
+-------+------------------+------+------------------+
```
🚀 **Perfect for identifying missing values, patterns, and outliers in numerical data!**  

---

### 🎯 **Key Takeaways**  
✅ **Transformations modify the DataFrame but do not execute immediately**.  
✅ **Actions trigger computations and return results** to the driver.  
✅ **Sorting, filtering, grouping, and renaming enhance structured data processing**.  
✅ **Summary statistics help detect outliers and data inconsistencies**.  

---

# 🔍 Lab 1: Inspecting Data in PySpark DataFrame 🚀  

## 📝 Overview  
Before analyzing data (plotting, modeling, training), it's **crucial** to **inspect** it. In this lab, we’ll examine the `people_df` DataFrame using fundamental PySpark operations.  

✅ **Print the first 10 observations**  
✅ **Count the number of rows**  
✅ **Identify the number of columns & their names**  

---

## ⚙️ Loading the Data  

We start by **reading the CSV file** and creating a PySpark **DataFrame**:  

```python
file_path = "file:///home/talentum/test-jupyter/P2/M3/sm2/2_OperatingonDataFramesinPySpark/Dataset/people.csv"

# Load data into a DataFrame
people_df = spark.read.csv(file_path, header=True, inferSchema=True)
```

---

## 📌 Inspecting Data  

### 🔹 **Step 1: View First 10 Rows**  
To quickly glance at the **top 10 records**, we use `.show(10)`:  

```python
# Print the first 10 observations 
people_df.show(10)
```

📌 **Output:**  
```
+---+---------+----------------+------+-------------+
|_c0|person_id|            name|   sex|date of birth|
+---+---------+----------------+------+-------------+
|  0|      100|  Penelope Lewis|female|   1990-08-31|
|  1|      101|   David Anthony|  male|   1971-10-14|
|  2|      102|       Ida Shipp|female|   1962-05-24|
|  3|      103|    Joanna Moore|female|   2017-03-10|
|  4|      104|  Lisandra Ortiz|female|   2020-08-05|
|  5|      105|   David Simmons|  male|   1999-12-30|
|  6|      106|   Edward Hudson|  male|   1983-05-09|
|  7|      107|    Albert Jones|  male|   1990-09-13|
|  8|      108|Leonard Cavender|  male|   1958-08-08|
|  9|      109|  Everett Vadala|  male|   2005-05-24|
+---+---------+----------------+------+-------------+
```

---

### 🔹 **Step 2: Count Total Rows**  
To **check data size**, we use `.count()`:  

```python
# Count the number of rows 
print("There are {} rows in the people_df DataFrame.".format(people_df.count()))
```

📌 **Output:**  
```
There are 100000 rows in the people_df DataFrame.
```

---

### 🔹 **Step 3: Check Columns & Their Names**  
To **list the column names and count them**, we use `.columns` and `len()`:  

```python
# Count the number of columns and their names
print("There are {} columns in the people_df DataFrame and their names are {}".format(len(people_df.columns), people_df.columns))
```

📌 **Output:**  
```
There are 5 columns in the people_df DataFrame and their names are ['_c0', 'person_id', 'name', 'sex', 'date of birth']
```

---

## 🎯 Key Takeaways  
✅ **Dataset loaded successfully!**  
✅ **Contains 100,000 rows** and **5 columns** (`_c0, person_id, name, sex, date of birth`).  
✅ **First 10 rows previewed** for inspection.  

📌 **Next Steps:** Now that we **inspected** the data, we can proceed with **data transformations, filtering, and analysis!** 🚀  

---

# ✨ Lab 2: PySpark DataFrame Subsetting & Cleaning  

## 📝 Overview  
Once we **inspect** the dataset, the next step is **cleaning**. This involves:  

✅ **Subsetting** specific columns  
✅ **Removing duplicate rows**  
✅ **Counting rows before & after cleaning**  

---

## ⚙️ Loading the Data  

We first **read the CSV file** to create a PySpark **DataFrame**:  

```python
file_path = "file:///home/talentum/test-jupyter/P2/M3/sm2/2_OperatingonDataFramesinPySpark/Dataset/people.csv"

# Load data into a DataFrame
people_df = spark.read.csv(file_path, header=True, inferSchema=True)
```

---

## 🎯 Subsetting Relevant Columns  

Since we only need **'name', 'sex', and 'date of birth'**, we use `.select()`:  

```python
# Select name, sex, and date of birth columns
people_df_sub = people_df.select('name', 'sex', 'date of birth')
```

---

## 📌 Inspecting Data  

### 🔹 **Step 1: View First 10 Rows**  
To **quickly check** the top 10 records, we use `.show(10)`:  

```python
# Print the first 10 observations from people_df_sub
people_df_sub.show(10)
```

---

## ❌ Removing Duplicate Entries  

### 🔎 **Step 2: Drop Duplicates**  
To remove duplicate entries from `people_df_sub`, we use `.dropDuplicates()`:  

```python
# Remove duplicate entries
people_df_sub_nodup = people_df_sub.dropDuplicates()
```

---

## 🔢 Comparing Row Counts  

### 🔹 **Step 3: Count Rows Before & After**  

```python
# Count the number of rows
print("There were {} rows before removing duplicates, and {} rows after removing duplicates".format(people_df_sub.count(), people_df_sub_nodup.count()))
```

📌 **This helps verify how many duplicates were removed!**

---

## 🔍 Identifying Duplicate Entries  

### 🔹 **Step 4: Find Duplicate Rows**  

```python
# Group by 'name', 'sex', 'date of birth' and count occurrences
df1 = people_df_sub.groupBy('name', 'sex', 'date of birth').count()

# Show duplicate entries
duplicates = df1.where('count > 1')
duplicates.show(10)
```

📌 This allows us to check **which rows** appear **more than once**.

---

## 🔄 Alternate Method to Show Duplicates  

```python
# Display rows that were removed
people_df_sub.exceptAll(people_df_sub_nodup).show()
```

📌 This gives a **direct view** of the duplicate rows that were removed.

---

## 🎯 Key Takeaways  
✅ **Dataset successfully cleaned!**  
✅ **Subsetted relevant columns (`name`, `sex`, `date of birth`)**  
✅ **Removed duplicate entries**  
✅ **Verified row count changes before & after cleaning**  

📌 **Next Steps:** Now that data is **clean**, we can perform **analysis & transformations!** 🚀  

---

# 🔍 Lab 3: Filtering Data in PySpark DataFrame 🚀  

## 📝 Overview  
In the previous exercise, we **subsetted data column-wise** using `.select()`. Now, we'll filter rows based on **specific conditions**, such as selecting:  

✅ **Only female records**  
✅ **Only male records**  
✅ **Counting the number of rows in each dataset**  

---

## ⚙️ Loading the Data  

As always, we first **load the CSV file** into a PySpark **DataFrame**:  

```python
file_path = "file:///home/talentum/test-jupyter/P2/M3/sm2/2_OperatingonDataFramesinPySpark/Dataset/people.csv"

# Load data into a DataFrame
people_df = spark.read.csv(file_path, header=True, inferSchema=True)
```

---

## 🎯 Filtering Records by Sex  

### 🔹 **Step 1: Select Only Female Entries**  
Using `.filter()`, we extract rows where `"sex"` is `"female"`:  

```python
# Filter people_df to select only female records
people_df_female = people_df.filter(people_df.sex == "female")
```

---

### 🔹 **Step 2: Select Only Male Entries**  
Similarly, we extract rows where `"sex"` is `"male"`:  

```python
# Filter people_df to select only male records
people_df_male = people_df.filter(people_df.sex == "male")
```

---

## 🔢 Counting Rows in Each Filtered DataFrame  

### 🔎 **Step 3: Count Female & Male Records**  

```python
# Count rows in each DataFrame
print("There are {} rows in the people_df_female DataFrame and {} rows in the people_df_male DataFrame".format(people_df_female.count(), people_df_male.count()))
```

📌 **Output:**  
```
There are 49,014 rows in the people_df_female DataFrame and 49,066 rows in the people_df_male DataFrame.
```

📌 The slight difference in row count **suggests that our dataset is nearly balanced between male & female records.**

---

## 🎯 Key Takeaways  
✅ **Filtered data efficiently using `.filter()`**  
✅ **Created separate DataFrames for male & female records**  
✅ **Counted rows in each filtered dataset**  

📌 **Next Steps:** We can now perform **further analysis** on each subset, such as checking age distributions or running demographic trends! 🚀  

---

# ⚡ Interacting with DataFrames Using PySpark SQL  

## 🔍 DataFrame API vs SQL Queries  

In **PySpark**, you can interact with **Spark SQL** using **two approaches**:  

✅ **DataFrame API** (Programmatic Domain-Specific Language - DSL)  
✅ **SQL Queries** (Concise & Portable)  

### 🎯 When to Use Each?  

🔹 **DataFrame API:**  
   - **Best for transformations & actions**  
   - Easier for **programmatic execution**  
   - Works well with **Spark’s distributed nature**  

🔹 **SQL Queries:**  
   - **Readable, familiar syntax** (especially for SQL users)  
   - **Portable across databases**  
   - Works seamlessly within **Spark environments**  

📌 **You can use SQL queries to perform operations on PySpark DataFrames!**  

---

## 🔄 Executing SQL Queries  

PySpark allows executing SQL **directly** using `.sql()` within `SparkSession`.  

```python
# Execute SQL queries using SparkSession
df.createOrReplaceTempView("table1")  # Stores the table in MetaStore.

df2 = spark.sql("SELECT field1, field2 FROM table1")
df2.collect()
```

📌 **Output:**  
```
[Row(f1=1, f2='row1'), Row(f1=2, f2='row2'), Row(f1=3, f2='row3')]
```

🚨 **Note:** Hive Metastore **must be running** for SQL-based querying!

---

## 🔍 Extracting Data Using SQL Queries  

### 🎯 Example Query  
```python
test_df.createOrReplaceTempView("test_table")

query = '''SELECT Product_ID FROM test_table'''
test_product_df = spark.sql(query) 
test_product_df.show(5)
```

📌 **Output:**  
```
+----------+
|Product_ID|
+----------+
| P00069042|
| P00248942|
| P00087842|
| P00085442|
| P00285442|
+----------+
```

🚀 **Quick retrieval of specific columns!**  

---

## 📊 Summarizing & Grouping Data Using SQL Queries  

### 🎯 Example: Find Maximum Purchase Per Age Group  

```python
test_df.createOrReplaceTempView("test_table")
query = '''SELECT Age, max(Purchase) FROM test_table GROUP BY Age'''
spark.sql(query).show(5)
```

📌 **Output:**  
```
+-----+-------------+
| Age | max(Purchase) |
+-----+-------------+
|18-25| 23958 |
|26-35| 23961 |
| 0-17| 23955 |
|46-50| 23960 |
|51-55| 23960 |
+-----+-------------+
```

📌 **Data is grouped & aggregated efficiently using SQL syntax!**  

---

## 🔎 Filtering Columns Using SQL Queries  

### 🎯 Example: Select Female Users with Purchases Over 20,000  

```python
test_df.createOrReplaceTempView("test_table")

query = '''SELECT Age, Purchase, Gender FROM test_table WHERE Purchase > 20000 AND Gender == "F"'''
spark.sql(query).show(5)
```

📌 **Output:**  
```
+-----+--------+------+
| Age | Purchase | Gender |
+-----+--------+------+
|36-45| 23792 | F |
|26-35| 21002 | F |
|26-35| 23595 | F |
|26-35| 23341 | F |
|46-50| 20771 | F |
+-----+--------+------+
```

📌 **Easy filtering with SQL conditions!**  

---

## 🎯 Key Takeaways  

✅ **PySpark SQL enables seamless querying within Spark environments!**  
✅ **Use DataFrame API for programmatic execution & SQL for concise data manipulation.**  
✅ **SQL queries allow aggregation, filtering, and extraction of structured data efficiently.**  

📌 **Next Steps:** We can now explore **joining tables, performing complex aggregations, and optimizing queries!** 🚀  

---

# ⚡ Lab 1: Running SQL Queries Programmatically  

## 📝 Overview  
PySpark allows you to **run SQL queries** directly on DataFrames using the `sql()` function.  
By leveraging **SparkSession**, you can:  

✅ **Create temporary tables** from PySpark DataFrames  
✅ **Run SQL queries programmatically**  
✅ **Store results in new DataFrames** for further analysis  

---

## ⚙️ Loading the Data  

First, we load the CSV file into a PySpark **DataFrame**:  

```python
file_path = "file:///home/talentum/test-jupyter/P2/M3/SM3/3_InteractingwithDataFramesusingPySparkSQL/Dataset/people.csv"

# Load data into a DataFrame
people_df = spark.read.csv(file_path, header=True, inferSchema=True)
```

---

## 🎯 Creating a Temporary Table  

A **temporary table** acts as a **pointer** to our DataFrame, enabling SQL operations:  

```python
# Create a temporary table "people"
people_df.createOrReplaceTempView("people")
```

📌 **This step makes 'people' accessible for SQL queries!**  

---

## 🔍 Executing SQL Query  

### 🔹 **Step 1: Select Names from Temporary Table**  
```python
# Construct SQL query
query = '''SELECT name FROM people'''

# Assign query results to a new DataFrame
people_df_names = spark.sql(query)
```

📌 **Now, `people_df_names` holds only the names from our dataset!**  

---

## 📌 Inspecting the Query Results  

### 🔎 **Step 2: Print the First 10 Names**  
```python
# Display the top 10 names
people_df_names.show(10)
```

📌 **Output:**  
```
+-----------------+
|             name|
+-----------------+
|   Penelope Lewis|
|    David Anthony|
|        Ida Shipp|
|     Joanna Moore|
|   Lisandra Ortiz|
|    David Simmons|
|    Edward Hudson|
|     Albert Jones|
| Leonard Cavender|
|   Everett Vadala|
+-----------------+
```

📌 **SQL queries return DataFrames, which can be further processed!**  

---

## 🎯 Key Takeaways  

✅ **Successfully executed SQL queries on PySpark DataFrames**  
✅ **Created a temporary table (`people`) for querying**  
✅ **Extracted and displayed names using SQL**  
✅ **Results returned as a new DataFrame (`people_df_names`) for further analysis**  

📌 **Next Steps:** Try running **more advanced SQL queries** like grouping, filtering, or aggregations! 🚀  

---

# 🔍 Lab 2: Filtering Data Using SQL Queries 🚀  

## 📝 Overview  
Now that we've run a **basic SQL query**, let's move to **more advanced filtering**!  
We’ll:  

✅ **Filter the dataset** by gender (`male` & `female`) using SQL  
✅ **Create separate DataFrames** for filtered records  
✅ **Count rows in each filtered dataset**  

---

## ⚙️ Loading the Data  

As always, we **load the CSV file** into a PySpark **DataFrame**:  

```python
file_path = "file:///home/talentum/test-jupyter/P2/M3/SM3/3_InteractingwithDataFramesusingPySparkSQL/Dataset/people.csv"

# Load data into a DataFrame
people_df = spark.read.csv(file_path, header=True, inferSchema=True)
```

---

## 🏗️ Creating a Temporary Table  

Before running SQL queries, we create a **temporary table** for `people_df`:  

```python
# Create a temporary table "people"
people_df.createOrReplaceTempView("people")
```

📌 **Now, we can query the DataFrame using SQL statements!**  

---

## 🔍 Filtering Data Using SQL Queries  

### 🔹 **Step 1: Select Female Records**  
```python
# Filter people table to select only female records
people_female_df = spark.sql('SELECT * FROM people WHERE sex=="female"')
```

---

### 🔹 **Step 2: Select Male Records**  
```python
# Filter people table to select only male records
people_male_df = spark.sql('SELECT * FROM people WHERE sex=="male"')
```

---

## 🔢 Counting Rows in Each Filtered DataFrame  

### 🔎 **Step 3: Count Female & Male Records**  

```python
# Count rows in each DataFrame
print("There are {} rows in the people_female_df and {} rows in the people_male_df DataFrames".format(people_female_df.count(), people_male_df.count()))
```

📌 **Output:**  
```
There are 49,014 rows in the people_female_df and 49,066 rows in the people_male_df DataFrames.
```

📌 The **row count difference** suggests a nearly **balanced dataset** in terms of gender representation.  

---

## 🎯 Key Takeaways  

✅ **Used SQL queries to filter DataFrames based on specific conditions!**  
✅ **Created separate DataFrames (`people_female_df`, `people_male_df`) for gender filtering**  
✅ **Counted rows for validation**  

---

# 🚀 Introduction to Data Cleaning with Apache Spark  

## 📝 What is Data Cleaning?  

Data cleaning is the **process of preparing raw data** for efficient use in **data processing pipelines**. Common tasks include:  

✅ **Reformatting or replacing text** (standardizing input values)  
✅ **Performing calculations** (converting units, applying transformations)  
✅ **Removing garbage or incomplete data** (handling missing values)  

📌 **Ensuring data integrity improves analysis and model accuracy!**  

---

## ⚡ Why Perform Data Cleaning with Spark?  

Traditional data systems **struggle** with performance and data flow organization.  
Apache Spark solves these issues by offering:  

✅ **Scalability** – Handles **large datasets efficiently** via **distributed processing**  
✅ **Lazy Evaluation** – Executes transformations **only when needed**, optimizing performance  
✅ **Powerful Data Handling** – Built-in **resilient** and **fault-tolerant** capabilities  

📌 **Spark simplifies large-scale data cleaning while boosting speed & efficiency!**  

---

## 🔍 Data Cleaning Example  

### 📌 **Raw Data (Before Cleaning)**  
```
name              age (years)       city  
---------------------------------------
Smith, John         37           Dallas  
Wilson, A.          59           Chicago  
null               215            (invalid)
```

### ✅ **Cleaned Data (After Processing)**  
```
last name      first name    age (months)   state  
-------------------------------------------------
Smith           John           444         TX  
Wilson          A              708         IL  
```

### 💡 **Key Transformations:**  
🔹 **Splitting names** into **first** and **last**  
🔹 **Converting age** from **years to months**  
🔹 **Standardizing city names to state abbreviations**  
🔹 **Removing garbage/missing values**  

📌 **Data is now structured & ready for analysis!**  

---

## 🔧 Spark Schemas  

### 🏗️ **Why Use Schemas?**  

✅ **Defines DataFrame structure**  
✅ **Supports multiple data types** (strings, dates, integers, arrays)  
✅ **Filters garbage data during import**  
✅ **Boosts performance** via **optimized storage & lazy evaluation**  

📌 **Schemas help maintain data integrity while improving query speed!**  

---

## 🏗️ Example Spark Schema  

Spark **schemas** always follow a `StructType` format.  
All **Spark data types** are sourced from the `pyspark.sql.types` package.  

### 🔹 **Defining a Schema in PySpark**  
```python
from pyspark.sql.types import StructType, StructField, StringType, IntegerType

# Define custom schema
peopleSchema = StructType([
    StructField('name', StringType(), True),   # Name column (string)
    StructField('age', IntegerType(), True),   # Age column (integer)
    StructField('city', StringType(), True)    # City column (string)
])
```

### 🔹 **Reading a CSV File Using Schema**  
```python
# Load CSV data with predefined schema
people_df = spark.read.format('csv').load("rawdata.csv", schema=peopleSchema)
```

📌 **Best Practice:** Always define **your own schema** instead of relying on **Spark’s default inference**!  

---

## 🎯 Key Takeaways  

✅ **Data cleaning is critical for reliable analysis**  
✅ **Apache Spark enables scalable, efficient data transformation**  
✅ **Schemas improve performance & data quality**  
✅ **Programmatically defining schemas optimizes pipeline execution**  

---

------------------------LAB----------------------------

---

# Immutability and 
Lazy Processing

## Variable review
Python variables:
Mutable
Flexibility
Potential for issues with concurrency
Likely adds complexity

## Immutability
Immutable variables are:
A component of functional programming
Defined once
Unable to be directly modified
Re-created if reassigned
Able to be shared ef f i ciently

---

## Lazy Processing
Isn't this slow?
Transformations
Actions
Allows efficient planning
voter_df = voter_df.withColumn('fullyear', 
voter_df.year + 2000)
voter_df = voter_df.drop(voter_df.year)
voter_df.count()

---

## Understanding 
Parquet

## Difficulties with CSVfiles
No defined schema
Nested data requires special handling 
Encoding format limited

---

## Spark and CSVfiles
Slow to parse: Because of row oriented nature
Files cannot be filtered (no "predicate pushdown")
Any intermediate use requires redefining schema

---

## The Parquet Format
A columnar data format
Supported in Spark and other data processing frameworks
Supports predicate pushdown
Automatically stores schema information

---

Working with Parquet
Reading Parquet files
df = spark.read.format('parquet').load('filename.parquet')
df = spark.read.parquet('filename.parquet')
Writing Parquet files
df.write.format('parquet').save('filename.parquet')
df.write.parquet('filename.parquet')

---

## Parquet and SQL
Parquet as backing stores for SparkSQL operations
flight_df = spark.read.parquet('flights.parquet')
flight_df.createOrReplaceTempView('flights')
short_flights_df = spark.sql('SELECT * FROM flights WHERE flightduration < 100')

---

------------------------LAB-----------------------------

---

Writing Parquet files
df.write.format('parquet').save('filename.parquet')
df.write.parquet('filename.parquet')

Using this format, use people.csv, create schema
load the data into dataframe
2. using this api, you are going to store that particular data on local file system insid your home, name of the folder will be people_csv > df1.write.format('csv').save('people_csv')
df2 = load the data from this particular location
store the data in another folder
design schema for df2 with 3 columns: id name and age and then show it and then store it in the file system in another location
