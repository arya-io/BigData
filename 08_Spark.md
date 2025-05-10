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

## Understanding SparkContext

SparkContext is an entry point into the world of Spark
An entry point is away of connecting to Sparkcluster
An entry point is like a key to the house
PySpark has adefault SparkContext called sc
A SparkContext represents the entry point to Spark functionality. It's like a key to your car. PySpark automatically creates a SparkContext for you in the PySpark shell (so you don't have to create it by yourself) and is exposed via a variable sc.

# script.py

# Print the version of SparkContext
print("The version of Spark Context in the PySpark shell is", sc.version)

# Print the Python version of SparkContext
print("The Python version of Spark Context in the PySpark shell is", sc.pythonVer)

# Print the master of SparkContext
print("The master of Spark Context in the PySpark shell is", sc.master)

The version of Spark Context in the PySpark shell is 2.4.5
The Python version of Spark Context in the PySpark shell is 3.6
The master of Spark Context in the PySpark shell is local[*]


## Inspecting Spark Context

Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 2.4.5
      /_/

Using Python version 3.6.9 (default, Mar 10 2023 16:46:00)
SparkSession available as 'spark'.

>>> id(sc)
139771463232984

>>> type(sc)
<class 'pyspark.context.SparkContext'>

Version: To retrieve SparkContext version
>>> sc.version
'2.4.5'

PythonVersion: To retrieve Python version of SparkContext
>>> sc.pythonVer
'3.6'

Master: URL of the cluster or “local” string to run in local mode of SparkContext
>>> sc.master
'local[*]'


## Loading data in PySpark

SparkContext's parallelize() method
rdd = sc.parallelize([1,2,3,4,5])

SparkContext's textFile() method
rdd2 = sc.textFile("test.txt")

File Protocol

jupyter notebook is not a spark shell
read evaluate print loop (REPL) is same as Spark Shell

## Interactive Use of PySpark

    Spark comes with an interactive python shell in which PySpark is already installed in it. PySpark shell is useful for basic testing and debugging and it is quite powerful. The easiest way to demonstrate the power of PySpark’s shell is to start using it.
    The most important thing to understand here is that we are not creating any SparkContext object because PySpark automatically creates the SparkContext object named sc, by default in the PySpark shell.

    # Create a python list of numbers from 1 to 100 
numb = range(1,101)
print(type(numb))

# Load the list into PySpark  
spark_data = sc.parallelize(numb)
print(type(spark_data))

# spark_data.collect()
print(spark_data.collect())

help(spark_data.collect())

## Loading data in PySpark shell

    In PySpark, we express our computation through operations on distributed collections that are automatically parallelized across the cluster.

    file_path = 'file:////home/talentum/spark/README.md'
# Load a local file into PySpark shell
lines = sc.textFile(file_path)
print(lines.take(5))

file_path = 'file:////home/talentum/spark/README.md'

# Load a local file into PySpark shell

lines = sc.textFile(file_path)

print(lines.take(5))

['# Apache Spark', '', 'Spark is a fast and general cluster computing system for Big Data. It provides', 'high-level APIs in Scala, Java, Python, and R, and an optimized engine that', 'supports general computation graphs for data analysis. It also supports a']

print(type(lines.take))
print(type(lines.take(5)))

<class 'method'>
<class 'list'>

lines.first()

'We the People of the United States, in Order to form a more perfect 

type(lines.first())
str

In Rdd, every line is known as an element.

---

# Use of Lambda function in python filter()

## What are anonymous functions in Python?
Lambda functions are anonymous functions in Python
Very powerful and used in Python. Quite effcient with map() and filter()
Lambda functions create functions to be called later similar to def
It returns the functions without any name (i.e anonymous)
Inline a function definition or to defer execution of acode

---

## Lambda function syntax
The general form of lambda functions is
lambda arguments: expression
Example of lambda function
double = lambda x: x * 2 
print(double(3))

---

## Difference between def vs lambda functions
Python code to illustrate cube of anumber
def cube(x):
return x ** 3
g = lambda x: x ** 3
print(g(10)) 
print(cube(10))
1000
1000

No return statement for lambda
Can put lambda function anywhere

---

## Use of Lambda function in python - map()
map() function takes a function and a list and returns a new list which contains items returned by that function for each item

General syntax of map()
map(function, list)

Example ofmap()

items = [1, 2, 3, 4] 
list(map(lambda x: x + 2 , items))

[3, 4, 5, 6]

The type of map is a Map Object.

The same functionality can be implemented using for loop. But that approach is verbose. So, in order to eliminate the verbosity, map function comes into picture.

---

## Use of Lambda function in python - filter()

Lambda function is also known as inline function.

filter() function takes a function and a list and returns a new list for which the function evaluates as true

General syntax of filter():
filter(function, list)

Example of filter()
items = [1, 2, 3, 4]
list(filter(lambda x: (x%2 != 0), items))

[1, 3]

Lambda Function is not a feature of Spark

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

## Decomposing RDDs
Resilient DistributedDatasets
Resilient: Abilityto withstandfailures
Distributed:Spanningacross multiplemachines
Datasets:Collectionofpartitioneddatae.g,Arrays,Tables,Tuplesetc.,

---

## Creating RDDs. How to do it?

Parallelizing anexistingcollectionofobjects
Externaldatasets: 
  Files in HDFS
  Objects in AmazonS3bucket 
  lines in a text file
From existingRDDs

---

## Parallelized collection(parallelizing)
parallelize() forcreatingRDDs frompythonlists
numRDD = sc.parallelize([1,2,3,4])
helloRDD = sc.parallelize("Hello world")
type(helloRDD)
<class 'pyspark.rdd.PipelinedRDD'>

---

## From external datasets
textFile() forcreatingRDDs fromexternaldatasets
fileRDD = sc.textFile("README.md")
type(fileRDD)
<class 'pyspark.rdd.PipelinedRDD'>

---

## Understanding Partitioning inPySpark
A partition isa logical division ofalargedistributeddataset
parallelize() method
numRDD = sc.parallelize(range(10), numSlices = 6)
textFile() method
fileRDD = sc.textFile("README.md", minPartitions = 6)
Thenumberofpartitionsin anRDD canbefound byusing getNumPartitions() method

rdd.glom()

hdfs fsck /user/talentum/stocks.csv -files -blocks -locations

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

## RDD Actions
Operation return avalueafterrunning acomputation ontheRDD
BasicRDD Actions
collect()
take(N) 
hrst() 
count()

---

## collect() and take()Actions
collect() return all the elements of the dataset as an array 
take(N) returns anarray with thehrstN elements ofthedataset
RDD_map.collect()
[1, 4, 9, 16]
RDD_map.take(2)
[1, 4]

---

## first() andcount() Actions
hrst() printsthehrstelementoftheRDD
RDD_map.first()
[1]
count() returnthenumberofelements in theRDD
RDD_flatmap.count()
5

---

Lab:

numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
numbRDD = sc.parallelize(numbers)

# Create map() transformation to cube numbers
cubedRDD = numbRDD.map(lambda x: x ** 3)

# Collect the results
numbers_all = cubedRDD.collect()

# Print the numbers from numbers_all
for numb in numbers_all:
    print(numb)

Output:
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

---

file_path = 'file:////home/talentum/spark/README.md'

# Create a fileRDD from file_path
fileRDD = sc.textFile(file_path)

# Filter the fileRDD to select lines with Spark keyword
fileRDD_filter = fileRDD.filter(lambda line: 'Spark' in line)

# How many lines are there in fileRDD?
print("The total number of lines with the keyword Spark is", fileRDD_filter.count())

# Print the first four lines of fileRDD
for line in fileRDD_filter.take(4): 
  print(line)

Output:
The total number of lines with the keyword Spark is 19
# Apache Spark
Spark is a fast and general cluster computing system for Big Data. It provides
rich set of higher-level tools including Spark SQL for SQL and DataFrames,
and Spark Streaming for stream processing.

---

## Introduction to pair RDDs in PySpark
Real lifedatasetsareusually key/valuepairs
Each rowis akeyandmapstooneormorevalues
Pair RDD is aspecialdatastructureto workwith thiskindofdatasets
Pair RDD: Key istheidentiherandvalueisdata

---

## Creating pairRDDs
TwocommonwaystocreatepairRDDs 
  From a list ofkey-valuetuple
  From a regularRDD
Get thedatainto key/valueformforpairedRDD

my_tuple = [('Sam', 23), ('Mary', 34), ('Peter', 25)] 
pairRDD_tuple = sc.parallelize(my_tuple)

my_list = ['Sam 23', 'Mary 34', 'Peter 25'] 
regularRDD = sc.parallelize(my_list)
pairRDD_RDD = regularRDD.map(lambda s: (s.split(' ')[0], s.split(' ')[1]))

---

## Transformations on pair RDDs
All regulartransformationsworkonpairRDD
Haveto passfunctions that operateonkeyvaluepairsratherthanonindividual elements
Examples ofpaired RDD Transformations
reduceByKey(func): Combinevalueswith thesamekey
groupByKey(): Group valueswith thesamekey
sortByKey(): Return anRDD sortedby thekey
join(): Join two pairRDDs basedontheirkey

---

## reduceByKey() transformation
reduceByKey() transformation combines valueswith thesamekey
It runsparalleloperationsforeachkeyin thedataset 
It isatransformationand not action
regularRDD = sc.parallelize([("Messi", 23), ("Ronaldo", 34),
("Neymar", 22), ("Messi", 24)]) 
pairRDD_reducebykey = regularRDD.reduceByKey(lambda x,y : x + y) 
pairRDD_reducebykey.collect()
[('Neymar', 22), ('Ronaldo', 34), ('Messi', 47)]

---

## sortByKey() transformation
sortByKey() operationorders pairRDD by key
It returns an RDD sortedby keyin ascendingordescendingorder
pairRDD_reducebykey_rev = pairRDD_reducebykey.map(lambda x: (x[1], x[0])) 
pairRDD_reducebykey_rev.sortByKey(ascending=False).collect()
[(47, 'Messi'), (34, 'Ronaldo'), (22, 'Neymar')]

---

## groupByKey() transformation
groupByKey() groupsallthevalueswith thesamekeyin thepairRDD
airports = [("US", "JFK"),("UK", "LHR"),("FR", "CDG"),("US", "SFO")]
regularRDD = sc.parallelize(airports) 
pairRDD_group = regularRDD.groupByKey().collect() 
for cont, air in pairRDD_group:
print(cont, list(air))
FR ['CDG']
US ['JFK', 'SFO'] 
UK ['LHR']

---

join() transformation
join() transformationjoinsthetwo pairRDDs basedontheirkey
RDD1 = sc.parallelize([("Messi", 34),("Ronaldo", 32),("Neymar", 24)])
RDD2 = sc.parallelize([("Ronaldo", 80),("Neymar", 120),("Messi", 100)])
RDD1.join(RDD2).collect()
[('Neymar', (24, 120)), ('Ronaldo', (32, 80)), ('Messi', (34, 100))]

---
































