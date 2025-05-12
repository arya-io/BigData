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

# More Actions

## reduce() action
reduce(func) action isusedforaggregatingtheelements ofaregularRDD
Thefunction should becommutative(changingtheorderoftheoperandsdoesnot changetheresult) 
andassociative
An exampleof reduce() action inPySpark
x = [1,3,4,6]
RDD = sc.parallelize(x) 
RDD.reduce(lambda x, y : x + y)
14

---

## saveAsTextFile() action
saveAsTextFile() action savesRDD into atexthleinsideadirectorywith eachpartition asa 
separatehle
RDD.saveAsTextFile("tempFile")
coalesce() methodcanbeusedtosaveRDD asasingletexthle


RDD.coalesce(1).saveAsTextFile("tempFile")
This is a transformation operation still generating a new RDD
---

## Action Operations on pair RDDs
RDD actionsavailable forPySparkpairRDDs
Pair RDD actionsleveragethekey-valuedata
FewexamplesofpairRDD actionsinclude
countByKey()
collectAsMap()

---

## countByKey() action
countByKey() only available fortype(K, V)
countByKey() action counts thenumberofelements for eachkey
Exampleof countByKey() onasimplelist
rdd = sc.parallelize([("a", 1), ("b", 1), ("a", 1)]) 
for kee, val in rdd.countByKey().items():
print(kee, val)
('a', 2)
('b', 1)


## collectAsMap() action
collectAsMap() returnthekey-valuepairsin theRDD asadictionary
Exampleof collectAsMap() onasimpletuple
sc.parallelize([(1, 2), (3, 4)]).collectAsMap()
{1: 2, 3: 4}



























