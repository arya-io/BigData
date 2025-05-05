# 📊 **MapReduce** Overview

MapReduce is an ETL (Extract, Transform, Load) framework where the program is written to process large data sets in parallel across a Hadoop cluster. It consists of two main phases:

### 1️⃣ **Map Phase: Collect Data**

* In this phase, the input data is processed into \<key, value> pairs.
* The input file is divided into smaller blocks, and each block is stored on different DataNodes across the Hadoop cluster.

![image](https://github.com/user-attachments/assets/f2265f8c-0ced-458c-840f-0466a63eee60)

### 2️⃣ **Shuffle/Sort Phase**

* The \<key, value> pairs from the Map phase are shuffled and sorted by key.
* Pairs with the same key are grouped together, and the values for each key are collected for further processing.

---

### 3️⃣ **Reduce Phase**

* The reducer processes the grouped data and outputs final \<key, value> pairs that are typically written to a file in HDFS.

![image](https://github.com/user-attachments/assets/520418aa-23ac-4080-84eb-066b6819a359)

---

## 🔍 **Understanding MapReduce** Step-by-Step

### 1️⃣ **Input File Breakdown**

* The input file is divided into blocks that are distributed across DataNodes in the Hadoop cluster.

![image](https://github.com/user-attachments/assets/0036978e-cc30-4158-aa68-841ceaf24453)

### 2️⃣ **Map Phase - Processing Data**

* Each map task processes a block of data (an Input Split).
* The map tasks are Java processes that run on the DataNodes where the data blocks are stored.

### 3️⃣ **\<Key, Value> Pair Generation**

* After processing the input, the map task outputs a set of \<key, value> pairs.

![image](https://github.com/user-attachments/assets/9b66e4a2-9418-4e5d-8efc-54a500d02986)

### 4️⃣ **Shuffle/Sort Phase**

* Records with the same key are grouped together and sent to the same reducer.
* The data is sorted by the key, and values are aggregated into collections.

### 5️⃣ **Reduce Phase - Output**

* The reducer processes each \<key, value> collection, performs the required computation, and outputs the final result.

---

## 📝 **Key/Value Pairs in MapReduce**

* The core of MapReduce is working with \<key, value> pairs.
* Mappers create these pairs, and reducers process them to generate final results.

![image](https://github.com/user-attachments/assets/9bbb4c7f-6a61-4556-92ea-6f10664421c2)

---

## 💡 **Example: WordCount in MapReduce**

One of the most common use cases of MapReduce is counting the frequency of words in a large text file.

### Steps:

1. **Input File**: The file can be large (MB to PB).
2. **Map Phase**: The mapper reads the file's blocks line-by-line.
3. **Splitting Words**: The lines are split into words, and \<word, 1> pairs are sent to the reducer.
4. **Shuffle/Sort Phase**: Pairs with the same word (key) are grouped together.
5. **Reduce Phase**: The reducer sums up all the "1"s for each word and outputs the word count.

![image](https://github.com/user-attachments/assets/a0ddf7c1-8d50-4639-8f9f-537d10f3e147)

---

## 🎥 **Demonstration: Running MapReduce**

Here’s how you can run a MapReduce job using Hadoop:

```bash
yarn jar /usr/hdp/2.6.0.3-8
```

![image](https://github.com/user-attachments/assets/5aa07f74-7737-46d1-be89-93fabb655804)

---

## 🖥️ **Executing the JAR File**

To execute a MapReduce job, you run a JAR file using `yarn`. Here’s a breakdown:

### Command:

```bash
yarn jar [path-to-jar] [job-name] [input] [output]
```

![image](https://github.com/user-attachments/assets/d010f6b8-9f8a-4f81-8b34-35df6f6b4b65)
![image](https://github.com/user-attachments/assets/950d4c01-7e37-4911-9608-b0f6428c551f)

---

## 📁 **Viewing the Output**

After executing the job, you can check the output directory to confirm the results:

### 1️⃣ **List the Files**:

```bash
hdfs dfs -ls wordcount_output
```

![image](https://github.com/user-attachments/assets/19eeeeda-431a-4b64-a96e-2cc7c6086ad9)

### 2️⃣ **View the Content**:

```bash
hdfs dfs -cat wordcount_output/part-r-00000
```

![image](https://github.com/user-attachments/assets/8271a8d3-2524-458a-84d2-53f8bc2646b3)

---

## 🌍 **Performing the MapReduce Task on BigDataVM**

On BigDataVM, we can execute the same WordCount MapReduce task using the Hadoop examples JAR. Here's the command:

### Command:

```bash
yarn jar ~/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount -D mapred.reduce.tasks=2 constitution.txt wordcount_output
```

This command runs the WordCount example on the `constitution.txt` file and outputs the result to `wordcount_output`.

![image](https://github.com/user-attachments/assets/60f7b43b-6f85-46a9-9cb8-02deb32e7936)
![image](https://github.com/user-attachments/assets/a2bd032d-185e-4971-b2f9-37539344a513)
![image](https://github.com/user-attachments/assets/774f7378-2f92-41bc-99bb-22f81e819265)

---

## 📦 **What is a .jar File?**

A `.jar` (Java ARchive) file is a compressed package that contains Java classes, metadata, and resources (like images or property files). It’s essentially a `.zip` file, but specifically for Java applications.

### Key Points:

* `.jar` files are used to bundle Java programs and their dependencies into a single file.
* They make it easier to distribute and run Java applications.

---

## 🔄 **Merging Files in Hadoop**

We merged the files in the `wordcount_output` directory into a single file in the `/tmp/final_op` directory using the following command:

```bash
hdfs dfs -getmerge wordcount_output /tmp/final_op
```

This is useful to combine smaller output files into one for easier processing or viewing.

![image](https://github.com/user-attachments/assets/a7444982-4838-4c6a-9f1a-d99513890575)
![image](https://github.com/user-attachments/assets/54483b22-c30d-432a-9c63-b83b8d36e8ea)

---

### 📝 **Word and Line Count of final\_op**

To verify the number of lines and words in the final output:

```bash
wc -l final_op
```

This gives the number of lines:

```
1683 final_op
```

To check the total number of words and characters:

```bash
wc final_op
```

This will show:

```
1683  3366 17049 final_op
```

![image](https://github.com/user-attachments/assets/201642ac-fc14-47c6-8eb6-24fa54b558e5)

---

## 🖥️ **Understanding the WordCountMapper Code**

### Code Overview

Here’s the code for the `WordCountMapper` class in Hadoop MapReduce:

```java
public class WordCountMapper
extends Mapper<LongWritable, Text, Text, IntWritable> { // This is generic

@Override

protected void map(LongWritable key, Text value,
Context context)
throws IOException, InterruptedException {
    String currentLine = value.toString();
    String[] words = currentLine.split(" ");
    for (String word : words) {
        Text outputKey = new Text(word);
        context.write(outputKey, new IntWritable(1));
    }
}
}
```

### **Explanation of the Code**

1. **Class Definition**

   ```java
   public class WordCountMapper extends Mapper<LongWritable, Text, Text, IntWritable>
   ```

   * The class extends `Mapper` with four generic types:

     * `LongWritable`: Represents the byte offset of the line in the input file.
     * `Text`: Represents the line of text being processed.
     * `Text`: The key (in this case, the word).
     * `IntWritable`: The value (initialized to `1`, representing the word count).

2. **Overriding the `map` Method**

   ```java
   @Override
   protected void map(LongWritable key, Text value, Context context)
   ```

   * The `map` method is called for each input record (in this case, each line of text).
   * It processes the input `key` (line offset) and `value` (the text of the line).

3. **Processing the Line**

   ```java
   String currentLine = value.toString();
   String[] words = currentLine.split(" ");
   ```

   * Converts the `Text` value (line of text) to a `String`.
   * Splits the line into individual words using a space (`" "`) as the delimiter.

4. **Emitting Key-Value Pairs**

   ```java
   for (String word : words) {
       Text outputKey = new Text(word);
       context.write(outputKey, new IntWritable(1));
   }
   ```

   * For each word in the line, it creates a `Text` object (representing the word).
   * It writes a key-value pair (`word`, `1`) to the context, which will be passed to the reducer.

---

### 🧠 **How It Works:**

* The **mapper** processes each line of input text.
* It splits the line into individual words.
* For each word, it emits a key-value pair: `(word, 1)`.
* These pairs are passed to the **reducer** to aggregate word counts.

---

## 🧑‍💻 **Explanation of the WordCountReducer Code**

The `WordCountReducer` class is responsible for aggregating word counts in the final output. Let’s break it down:

### 1️⃣ **Class Definition**

```java
public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable>
```

* It extends the `Reducer` class with the following generic types:

  * **`Text`**: Represents the key (the word).
  * **`IntWritable`**: Represents the value (the word count).
  * **`Text`**: Output key (the word).
  * **`IntWritable`**: Output value (final count of the word occurrences).

---

### 2️⃣ **Overriding the `reduce` Method**

```java
@Override
protected void reduce(Text key, Iterable<IntWritable> values, Context context)
```

* The `reduce` method is invoked for each unique word (key) emitted by the mapper.
* It receives the word (key) and a list of occurrences (values), where each occurrence is an `IntWritable` with value `1`.

---

### 3️⃣ **Summing Up Word Occurrences**

```java
int sum = 0;
for (IntWritable count : values) {
    sum += count.get();
}
```

* This loop iterates over the list of `IntWritable` values, each representing a `1` from the mapper.
* It sums up the occurrences of the word to get the total count.

---

### 4️⃣ **Writing the Final Word Count**

```java
IntWritable outputValue = new IntWritable(sum);
context.write(key, outputValue);
```

* After calculating the total word count, a new `IntWritable` is created with the summed value.
* It writes the final `(word, total count)` pair to the context, making it available for output.

---

### 🧠 **How It Works**

* The **reducer** receives a list of `(word, 1)` pairs from the mapper.
* It aggregates the occurrences of each word.
* It outputs the final result as `(word, total occurrences)` for further processing or storage.

This step finalizes the MapReduce job by summing and outputting the results.

---

## 🏃‍♂️ **Running a MapReduce Job**

To run a MapReduce job on Hadoop/YARN, follow these steps:

1. **Put Input Files into HDFS**
   Ensure that your input files are available in HDFS (Hadoop Distributed File System).

2. **Delete the Output Directory (if it exists)**
   If the output directory already exists, it should be deleted to avoid conflicts.

3. **Execute the Job**
   Use the `yarn` command to execute the MapReduce job:

   ```bash
   yarn jar [jarfilename] [package_name].[class_name] [textfile] [foldername to store the output]
   ```

   Example:

   ```bash
   yarn jar wordcount.jar my.WordCountJob input/file.txt result
   ```

4. **View the Output**
   After execution, you can check the output directory in HDFS to see the results of the MapReduce job.

---

## ⚙️ **Executable Jar vs Normal Jar**

An **Executable Jar** is a JAR file that contains a `main` method or entry point for execution. This type of JAR is used to run applications directly.

* **Normal JAR**: May contain libraries or resources without an entry point, often used as a dependency for other applications.
* **Executable JAR**: Includes a `main` method or is configured to be executed directly with the command `java -jar`.


---

## 📝 Shell Script Notes

### 📜 **Doc Comments**:

```bash
# Author: Priyanka
# Date Created: 03-05-2025
# Modification Date: 03-05-2025
# Description: This is the first nano file
# Usage: doc/test.sh
```

---

### 🖥️ **Text Editors**: `vim` vs `nano`

* **vim** and **nano** are command-line editors.
* **nano** is simpler and more user-friendly compared to **vim**.
* By default, **nano** has all installation features available.
* In **nano**,

  * `^` refers to the \[Ctrl] key.
  * `M` refers to the \[Alt] key.

### 💾 **Saving in Nano**:

To save a file in **nano**:

* Press `CTRL + O`, then `ENTER`, and finally `CTRL + X` to exit.

---

### 📝 **Shell Script Example**: `test.sh`

```bash
nano test.sh

#!/bin/bash

# Author: Priyanka
# Date Created: 03-05-2025
# Modification Date: 03-05-2025
# Description: This is the first nano file
# Usage: doc/test.sh

$(hdfs dfs -test -e /user/talentum/)

# if [[ $? -eq 0 ]]; then
#     echo "Path Exists..!!"
# else
#     echo "Path Doesn't Exists..!!"
# fi

a=$(echo "Hello")
echo $a
```

**Output**:

```bash
bash test.sh
Hello
```

![Nano Screenshot 1](https://github.com/user-attachments/assets/96d9fbb2-6e49-453d-9d0e-b8d21c4d0d6c)
![Nano Screenshot 2](https://github.com/user-attachments/assets/9b45997b-c57d-4eb3-bbf0-8fa87de20bcb)

---

### 🛠️ **Basic Conditions in Shell Scripts**

* After the `if` keyword, **use square brackets**.
* The command `hdfs dfs -ls` returns an **exit status** that indicates whether the command was successful.

---

### 🔁 **Functions & Code Reusability**

* **Avoid code repetition**—if the same block of code is used multiple times, create a **function** for it.
* You can also **create libraries of functions** for repeated tasks, making your code cleaner and more efficient.

---

### 🔄 **Flow of Execution Example**: Big Data Command

```bash
yarn jar invertedindex.jar <Main class> inverted/ inverted/output
```

**Flow**:

1. **Main Method**: The first method that gets triggered.
2. **ToolRunner**: Executes the `run()` method.

   * `Configuration conf = super.getConf();`
   * `Path in = new Path(args[0]);`
   * `Path out = new Path(args[1]);`
3. Input: `inverted` is `args[0]`.
4. Output: `inverted/output` is `args[1]`.
5. **Yarn**: Responsible for launching **Mapper** instances.

---

### **MapReduce Code Breakdown:**

---

### 📜 **Class `IndexInverterJob`**

This is the main class that extends `Configured` and implements `Tool`. It manages the execution of the MapReduce job.

* **Mapper Class**: `IndexInverterMapper`
* **Reducer Class**: `IndexInverterReducer`

The job is run through the `run()` method, which configures the MapReduce job, including setting input/output paths, mapper/reducer classes, and output formats.

---

### **Mapper Class**: `IndexInverterMapper`

```java
public static class IndexInverterMapper extends Mapper<LongWritable, Text, Text, Text> {

    private Text outputKey = new Text();
    private Text outputValue = new Text();

    // Map function to process input records
    @Override
    protected void map(LongWritable key, Text value, Context context)
            throws IOException, InterruptedException {
        // Split the input line by commas
        String [] words = value.toString().split(",");
        outputValue.set(words[0]); // The first word is the URL

        // For each of the remaining words, emit a key-value pair
        for(int i = 1; i < words.length; i++) {
            outputKey.set(words[i]); // The word
            context.write(outputKey, outputValue); // Emit word and URL
        }
    }
}
```

* **Input**: A line from the input file, split by commas.
* **Output**: For each word (except the first one), it creates an output key-value pair with the word as the key and the URL as the value.

---

### **Reducer Class**: `IndexInverterReducer`

```java
public static class IndexInverterReducer extends Reducer<Text, Text, Text, Text> {
    private Text outputValue = new Text();

    // Reduce function to merge values
    protected void reduce(Text key, Iterable<Text> values, Context context)
            throws IOException, InterruptedException {
        StringBuilder builder = new StringBuilder();
        for (Text value : values) {
            builder.append(value.toString()).append(","); // Append each URL
        }
        builder.deleteCharAt(builder.length() - 1); // Remove the last comma
        outputValue.set(builder.toString()); // Set the final value for the key
        context.write(key, outputValue); // Write the output (word, concatenated URLs)
    }
}
```

* **Input**: A word (key) and a list of URLs (values).
* **Output**: A single line with the word as the key and all associated URLs concatenated by commas.

---

### **Main Job Execution**: `run()` method

```java
public int run(String[] args) throws Exception {
    Configuration conf = super.getConf();
    Job job = Job.getInstance(conf, "IndexInverterJob");
    job.setJarByClass(IndexInverterJob.class);

    Path in = new Path(args[0]);
    Path out = new Path(args[1]);
    out.getFileSystem(conf).delete(out, true);
    FileInputFormat.setInputPaths(job, in);
    FileOutputFormat.setOutputPath(job,  out);

    // Set Mapper, Reducer, and other job settings
    job.setMapperClass(IndexInverterMapper.class);
    job.setReducerClass(IndexInverterReducer.class);

    job.setInputFormatClass(TextInputFormat.class);
    job.setOutputFormatClass(TextOutputFormat.class);

    job.setMapOutputKeyClass(Text.class);
    job.setMapOutputValueClass(Text.class);

    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);

    return job.waitForCompletion(true) ? 0 : 1;
}
```

* **Steps**:

  1. Set the input and output paths.
  2. Specify the Mapper and Reducer classes.
  3. Set the input/output formats (for text files).
  4. Set the map and output key/value types.
  5. Run the job and return the result.

---

### **Main Method**: `main()`

```java
public static void main(String[] args) {
    int result;
    try {
        result = ToolRunner.run(new Configuration(), new IndexInverterJob(), args);
        System.exit(result);
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

* **Executes the MapReduce job** using `ToolRunner` to configure and run the job, handling exceptions if any occur.

---

### 📝 **Original Dataset: `hortonworks.txt`**

The dataset contains rows where each line consists of a URL followed by a list of keywords, separated by commas. The goal is to create an inverted index that associates each keyword with all the URLs it appears in.

---

### **Expected Output**

For example, after running the job on the `hortonworks.txt` file, the output might look like this:

```
hadoop    http://hortonworks.com/,http://hortonworks.com/products/,http://hortonworks.com/kb,http://hortonworks.com/community/
hdp       http://hortonworks.com/products/,http://hortonworks.com/download/,http://hortonworks.com/get-started/,http://hortonworks.com/events/
platform  http://hortonworks.com/resources/,http://hortonworks.com/events/
...
```

* **Key**: A word (e.g., `hadoop`, `hdp`, `platform`)
* **Value**: A comma-separated list of URLs that contain the word.

---

### 🏁 **Run Command**

To run the application on YARN:

```bash
yarn jar invertedindex.jar <Main class> inverted/ inverted/output
```

* Replace `<Main class>` with the fully qualified class name (`inverted.IndexInverterJob`).
* `inverted/` is the input directory containing the `hortonworks.txt`.
* `inverted/output` is the output directory where the inverted index will be stored.

---

## 🧑‍💻 **Mapper Phase**:

* In the **Mapper Phase**, `k1` and `v1` are passed, and then `k2` and `v2` are generated.
* `k1` contains the **link (URL)**, and `v1` contains the associated **keywords**:

  ```plaintext
  k1 = link (e.g., http://hortonworks.com/)
  v1 = hadoop, webinars, articles, download, enterprise, team, reliability
  ```
* After the Mapper Phase, `k2` and `v2` are generated:

  * `k2` will be a **word** (e.g., "hadoop").
  * `v2` will be a **list of URLs** where the word appears:

    ```plaintext
    k2 = "hadoop"
    v2 = ["http://hortonworks.com/", "http://hortonworks.com/products/", "http://hortonworks.com/products/hortonworksdataplatform/", ...]
    ```

---

## 🔄 **Reducer Phase**:

The **Reducer** phase handles the aggregation of results:

```java
reduce(Text key, Iterable<Text> values, Context context)
```

* **`Text key`**: Represents the **word** (e.g., "hadoop").
* **`Iterable<Text> values`**: Contains the list of **URLs** (from the Mapper Phase) associated with that word.

In the Reducer:

1. **The key (word)** is the word passed from the Mapper.
2. **The values** are all URLs associated with that word, concatenated into a final result.

---

## 📁 **Output of the Program**:

The output of the program is stored in HDFS in the specified output directory. Here's an example of what you might see when you run:

```bash
hdfs dfs -cat IndexInverterJob_output/part-r-00000
```

The output will look like this, with each line representing a word and the list of URLs it is associated with:

```
about    http://hortonworks.com/about-us/
apache   http://hortonworks.com/products/hortonworksdataplatform/
apache   http://hortonworks.com/about-us/
articles http://hortonworks.com/community/
articles http://hortonworks.com/
...
```

* **Key (word)**: Each word from the input file.
* **Value (list of URLs)**: All the URLs where that word appears.

---

## 🖼️ **MapReduce Process Diagram**:

Here’s a visual representation of how data flows through the **MapReduce** framework, showcasing the **Mappers**, the intermediate stages, and the **Reducer** that aggregates results.

![image](https://github.com/user-attachments/assets/94daa7b8-aec6-4b52-8639-1895f8ed9824)

---

## 🖼️ **Breakdown of the MapReduce Diagram**:

1. **Input Split**:
   Data is divided into smaller chunks, making it easier to process in parallel across different nodes.

2. **InputFormat**:
   This step generates **`<k1, v1>`** key-value pairs from the input data for processing by the Mapper.

3. **Mapper**:
   The Mapper processes the **`<k1, v1>`** pairs and transforms them into **`<k2, v2>`** pairs, which are the output of the Mapper phase.

4. **Map Output Buffer**:
   Temporarily holds the output from the Mapper. Once the buffer reaches a certain threshold, the data is spilled to disk.

5. **Spill Files**:
   Once the buffer overflows, sorted records are written to spill files on disk.

6. **Merge Spill Files**:
   Multiple spill files are merged into one sorted file for efficient processing.

7. **Reducer Input**:
   The merged spill files become the input for the **Reducer** phase.

8. **Reducer**:
   The Reducer processes and aggregates values for each key and produces the final results.

---

## 🔑 **Key Points: Why This Process Is Important**:

* The flow helps explain **large-scale data processing** in Hadoop, making it easier to understand **data movement, storage, and computation**.
* By splitting work across multiple nodes, Hadoop optimizes processing, handling massive data efficiently.
* The **NodeManager** in the diagram plays a critical role in managing resources on the nodes.

### 🖼️ **Data Flow in Hadoop MapReduce**:

The diagram illustrates how data moves from the **Mapper** phase to the **Reducer** phase and then to the **HDFS**:

![image](https://github.com/user-attachments/assets/b0772637-dd21-40ce-bf9f-0adcc25fa694)

### **Key Steps in the Data Flow**:

1. **Reducer Fetches Data**:
   The **Reducer** retrieves data from the **Mapper output** (stored in buffers or spill files).

2. **In-Memory Buffer**:
   The fetched data is stored temporarily in memory.

3. **Spill Files Creation**:
   When the buffer reaches a threshold, the sorted data is written into spill files.

4. **Merging Spill Files**:
   Multiple spill files are merged into a single sorted file for efficient processing.

5. **Reducer Processing**:
   The merged data is processed by the **Reducer** to aggregate the results.

6. **Final Output to HDFS**:
   The Reducer produces the final results, which are stored in **HDFS**.

### **Key Components in the Image**:

* **NodeManager** → Manages execution and resource allocation on the nodes.
* **Buffer & Spill Files** → Intermediate storage before merging.
* **Merged Input** → The optimized data used by the **Reducer**.
* **HDFS Storage** → Where the final output is stored.

---

## 🧑‍💻 **About YARN**:

**YARN** (Yet Another Resource Negotiator) is a resource management layer in Hadoop 2.x, which helps improve resource utilization and job management.

### **How YARN Works**:

YARN splits the responsibilities of **JobTracker** (from Hadoop 1.x) into two separate components:

* **ResourceManager**:
  Allocates resources and schedules applications.

* **ApplicationMaster**:
  Executes applications and provides failover support.

---

## ⚙️ **JVM Process and Memory Management**:

* **ClassLoader**:
  Loads the classes required for execution into **RAM** memory.

* **JVM Process**:
  A **JVM process** is launched to run the application.

* **Stack and Heap**:

  * **Stack**: Stores method calls and local variables.
  * **Heap**: Stores objects and their data.

* **How a Program Runs**:

  * The **Main** method runs at the top of the stack.
  * Functions called inside the **Main** method are pushed on top of the stack.
  * After execution, functions are popped off the stack in the reverse order they were called.

* **Process Lifecycle**:
  Once the program terminates, it undergoes **de-processing** to free up resources.

---

This section provides a clear breakdown of the **MapReduce workflow**, the key role of **YARN**, and how the **JVM** manages memory during execution.

---

## 🛠️ **Open-Source YARN Use Cases**

* **Tez**: Enhances the execution of MapReduce jobs by providing a more efficient execution engine.
* **Slider**: Facilitates the deployment of existing distributed applications onto the YARN platform.
* **Storm**: A real-time computation framework, designed for processing real-time data streams.
* **Spark**: A MapReduce-like cluster computing framework, optimized for low-latency iterative jobs and interactive use through an interpreter.
* **Open MPI**: A high-performance message-passing library that implements the MPI-2 standard for parallel computing.
* **Apache Giraph**: A graph processing platform built for large-scale graph analytics in distributed environments.

---

## 🔧 **The Components of YARN**

The **ResourceManager** communicates with several components, including **NodeManagers**, **ApplicationMasters**, and **Client Applications**.

### 🖼️ **YARN Components and Their Interaction**:

![image](https://github.com/user-attachments/assets/b8fdf72a-9a89-4933-9fcf-2d5f29324cb5)

This image illustrates the architecture of **YARN** (Yet Another Resource Negotiator) in a **distributed computing environment**, showing the key components and their interactions.

### **Key Components:**

1. **ResourceManager** 🖥️

   * **Role**: The central authority that manages the allocation of resources across the cluster.
   * **Responsibilities**: Communicates with NodeManagers, ApplicationMasters, and Client Applications to ensure efficient resource distribution.

2. **NodeManager** ⚙️

   * **Role**: Manages resources on each individual node in the cluster.
   * **Responsibilities**: Reports available resources to the ResourceManager and executes tasks as directed.

3. **ApplicationMaster** 🔗

   * **Role**: Manages the execution of a specific application on YARN.
   * **Responsibilities**: Requests resources from the ResourceManager and monitors the lifecycle and progress of the application.

4. **Client Application** 🏢

   * **Role**: The external program that submits tasks or jobs to YARN.
   * **Responsibilities**: Sends job requests to the ResourceManager, specifying the required resources.

---

### **YARN Workflow Summary:**

1. A **Client Application** submits a job to the **ResourceManager**.
2. The **ResourceManager** assigns an **ApplicationMaster** to the job.
3. The **ApplicationMaster** requests resources from the **ResourceManager**.
4. Once resources are allocated, the job runs on different **NodeManagers** across the cluster.
5. The **NodeManagers** execute tasks and report their progress back to the **ResourceManager**.

---

### **Key Benefits of YARN's Architecture:**

* **Efficient Resource Allocation**:
  YARN ensures that resources are used optimally across the cluster by managing tasks dynamically.

* **Scalability**:
  YARN can scale to support large clusters with many nodes, making it suitable for big data applications.

* **Multi-Tenancy**:
  YARN supports the execution of multiple different types of applications, improving overall utilization of cluster resources.

---

This section emphasizes how YARN enables **efficient resource management**, **scalability**, and **multi-tenancy** in distributed data processing systems like **Hadoop**.

---

## 📅 **Lifecycle of a YARN Application**

![image](https://github.com/user-attachments/assets/011f7bfb-f514-49d7-a7b1-60d3ce41875d)

This image illustrates the **lifecycle of a YARN (Yet Another Resource Negotiator) application**, outlining the key steps in how a job is processed within a YARN-managed cluster.

### **Lifecycle Steps:**

1. **Client Submits Application** 📨

   * A **Client** submits a request to the **ResourceManager** to execute a job/application in the YARN cluster.

2. **ApplicationMaster Allocation** 🛠️

   * The **ResourceManager** locates a **NodeManager** with sufficient available resources.
   * A **NodeManager** creates a container to launch the **ApplicationMaster** (AM) for the job.

3. **ApplicationMaster Requests Resources** 🔄

   * The **ApplicationMaster** contacts the **ResourceManager** to request resources necessary to run the tasks for the application.
   * The **ResourceManager** then allocates and provides a list of containers where the tasks will run.

4. **Task Execution in Containers** 🚀

   * The **NodeManagers** launch the tasks within containers (which are essentially JVM instances).
   * The **ApplicationMaster** oversees the progress of tasks within containers and ensures that computation or data processing is happening as intended.

5. **Completion & Resource Cleanup** ✅

   * Upon the completion of tasks, the results are stored in the designated storage (HDFS or other systems).
   * Resources, including containers, are cleaned up and released back to the cluster for reuse.

---

### **Why This Matters?**

* YARN ensures **efficient cluster resource management**, enabling distributed applications to run effectively.
* By managing resources and scheduling tasks, **YARN** allows **multiple applications** to run concurrently without overloading the system, optimizing the use of resources.
* This process enables frameworks like **Hadoop** to efficiently handle **big data processing** across a large number of **nodes**, ensuring scalability and reliability.

---

### **Key Concept: Distributed Programming**

The entire YARN application lifecycle exemplifies **distributed programming**, where tasks are distributed across various nodes and resources in the cluster, ensuring parallel processing, resource optimization, and scalability in large-scale computing environments.

---

This section breaks down the **YARN lifecycle** and emphasizes the importance of **distributed programming** for efficient big data processing.

---

## 📊 **A Cluster View Example**

![image](https://github.com/user-attachments/assets/b57a8e01-85e7-48ba-9c53-366fc5e49ba4)

When accessing **localhost:8088** on a Linux browser, you will see a view like the one below:

![image](https://github.com/user-attachments/assets/d5e2a862-838b-403d-a18c-cef532ebb519)

In this view, multiple **application IDs** are displayed, showing how **YARN** manages and schedules applications within the cluster.

### **Key Components in the Cluster:**

1. **ResourceManager** 🖥️

   * Manages resources across the entire cluster.
   * Includes a **Scheduler** for resource allocation and an **ApplicationMaster Scheduler (AsM)** for handling application requests.

2. **NodeManager** ⚙️

   * Runs on each node in the cluster.
   * Monitors node resources and manages **Containers** that execute tasks.
   * Communicates with the **ResourceManager** to update resource status.

3. **Application Masters (AM)** 🔗

   * Each application has an associated **ApplicationMaster**.
   * The AM is responsible for managing the execution of the application, requesting resources, and monitoring progress.

4. **Containers** 📦

   * Containers are the isolated environments where application tasks are executed.
   * The **ResourceManager** dynamically allocates containers to nodes for task execution.
   * Some nodes may run both **Containers** and **ApplicationMasters**.

### **Cluster Structure Insights:**

* **Nodes with Containers:** These are responsible for executing the computational workloads.
* **Nodes with Application Masters:** These coordinate and monitor the execution of tasks.
* **Resource Allocation:** The **ResourceManager** optimizes resource distribution, and tasks are executed in parallel across different **containers** and **nodes**.

### **Why This Architecture is Useful?**

* **Scalability:** The architecture supports dynamic resource adjustments, allowing for flexible scaling in a distributed environment.
* **Efficiency:** Separating resource management (by ResourceManager) from task execution (by NodeManagers) ensures optimal performance.
* **Fault Tolerance:** If nodes fail, tasks can be redistributed to ensure uninterrupted execution.

---

# 🗂️ Map Aggregation – Simplifying Data Processing 🚀  

![image](https://github.com/user-attachments/assets/bc256336-986a-4f03-b8ea-5c69aa3dee5b)  

Map Aggregation plays a **key role** in optimizing MapReduce workflows by **reducing intermediate data transfer** between the Mapper and Reducer. Let’s break it down in **simple terms** and understand why it's so important!  

---

## ❌ Without Aggregation – Lots of Data, More Processing  
- The **Mapper** processes each word **individually**, generating separate key-value pairs.  
- Example key-value pairs produced by the Mapper:  
  - <"by", 1>, <"the", 1>, <"people", 1>  
  - <"for", 1>, <"the", 1>, <"people", 1>  
  - <"of", 1>, <"the", 1>, <"people", 1>  
- Since **every word occurrence** is sent as a separate entry, the **Reducer** has to deal with a **huge volume of data**, increasing:  
  - 📡 **Network traffic** (data transfer between Mapper & Reducer)  
  - ⏳ **Processing time** (Reducer takes longer to consolidate results)  

💡 **Analogy:** Imagine every student in a school submits their own attendance record separately, instead of the teacher summing them up before passing the total count to the office. The office now has **hundreds** of records instead of just one summary—making their job harder!  

---

## ✅ With Aggregation – Less Data, Faster Processing  
- The **Mapper** pre-processes the data, combining duplicate words before sending output to the Reducer.  
- Example key-value pairs after aggregation:  
  - <"by", 1>, <"the", 3>, <"people", 3>  
  - <"for", 1>, <"of", 1>  

### 🎯 **Why is this Better?**  
- **🚀 Faster Execution** – Less data means **quicker** transfers.  
- **🌐 Reduced Network Traffic** – The amount of intermediate data **shrinks**, leading to **smoother** processing.  
- **💰 Cost-Efficient** – Optimized workflow **reduces computational overhead** and saves resources.  

💡 **Analogy:** Instead of students submitting **individual attendance reports**, the teacher **tallies everything first** and submits just **one final count**—saving time and effort!  

---

## 🏁 **Final Thoughts**  
Aggregation **reduces redundant data movement** in MapReduce, making workflows **efficient and scalable**, especially when processing **massive datasets**!  

💭 **Remember:** If your data is **huge**, consider aggregation to **speed up** and **optimize** the process. 🚀  

---

# ⚡ Overview of Combiners – Optimizing MapReduce Efficiency 🚀  

![image](https://github.com/user-attachments/assets/eaaa1d77-0dac-4fbd-8f35-6e420bba14c5)  

The **Combiner** in Hadoop’s MapReduce framework plays a **crucial role** in optimizing **file I/O operations** and **reducing data transfer overhead**. Think of it as a **mini Reducer**, working at the Mapper level to **pre-process** data before it reaches the actual Reducer.  

---

## 🏗️ How It Works – Step by Step  

### 1️⃣ **MapOutputBuffer – Where It All Starts**  
- The **Mapper** processes data and holds the **key-value pairs** (`<k2,v2>`) in a **buffer**.  
- But buffers have **limits**! 🛑 Once full, the **data spills** to disk, causing extra I/O operations.  

💡 **Analogy:** Think of this like packing a suitcase. If you don’t organize items properly, you might end up stuffing too many bags, leading to unnecessary **baggage weight** (extra disk storage).  

---

### 2️⃣ **Combiner – Reducing the Load**  
- The **Combiner** steps in before the data hits the disk, grouping values locally.  
- It **acts like a Reducer**, **summarizing repeated values** before storage.  
- **Goal:** Reduce **data size** to minimize storage and **speed up** processing.  

💡 **Analogy:** Instead of throwing all items into your suitcase randomly, you neatly **fold and compress** clothes first, so fewer bags are needed! 🎒  

---

### 3️⃣ **Disk Spill Files – Less I/O, More Efficiency**  
- Since the **Combiner minimizes redundant records**, the disk stores **less data**.  
- The Mapper’s output eventually becomes the **Reducer’s input**, so **smaller spills mean faster execution**.  
- 🚀 **End result:** Less **I/O overhead**, **reduced network traffic**, and **optimized MapReduce performance**!  

💡 **Analogy:** If you’ve **pre-sorted** your clothes before packing, you have **fewer bags to carry**, making travel **lighter and smoother**. ✈️  

---

## 🎯 **Why is the Combiner Important?**  
✅ **Optimizes Disk Usage** – Less storage needed per Mapper output.  
✅ **Speeds Up Processing** – Data reaches the Reducer in **smaller chunks**.  
✅ **Reduces Network Load** – Less intermediate data means **faster transfers**.  
✅ **Boosts Hadoop Efficiency** – A must-have for **large-scale data** workflows!  

---

## 🏁 **Final Thoughts**  
The **Combiner** is a powerful **local optimization tool** that makes **MapReduce workflows scalable** and **cost-effective**. If your dataset is **large**, using a Combiner can **significantly cut down processing time**!  

---

# 🔄 Reduce-side Combining – Optimizing Data Flow in Hadoop 🚀  

![image](https://github.com/user-attachments/assets/54fecbc7-f554-46d3-b2aa-329192b0e5d2)  

Reduce-side Combining is a **crucial mechanism** in Hadoop’s **Reduce phase**, helping optimize the flow of **intermediate key-value pairs** and **minimizing shuffle data**. Let's break it down in simple terms!  

---

## 🏗️ **How Reduce-side Combining Works**  

### 1️⃣ **In-memory Buffer – First Stop**  
- Data processed by **Mappers** gets **stored in an in-memory buffer** before further processing.  
- The buffer **temporarily holds** intermediate results to **minimize direct disk writes**.  

💡 **Analogy:** Imagine gathering test results from different schools in a temporary spreadsheet before organizing them—this saves **time and effort**! 📊  

---

### 2️⃣ **Spill Files – Managing Large Data**  
- When the buffer **exceeds a threshold**, data spills to disk into **spill files**.  
- This prevents memory overflow and ensures **smooth processing**.  

💡 **Analogy:** Think of writing quick notes on a whiteboard. Once the board is full, you **copy the notes into a notebook**—that’s like spilling to disk! 📜  

---

### 3️⃣ **Merged Input – Organizing Data**  
- Multiple **spill files are merged** to create a single **structured input** for the Reducer.  
- This **reduces redundancy** and makes handling large datasets more **efficient**.  

💡 **Analogy:** Instead of storing separate spreadsheets for every school’s test results, you **merge them into one file**, making analysis **easier**. 🔄  

---

### 4️⃣ **Reducer – Final Processing**  
- The **Reducer processes the merged data**, performing **grouping and computation** to generate final results.  
- This is where **actual logic is applied**, such as counting words, aggregating sums, or computing statistics.  

💡 **Analogy:** Imagine grading all student scores after merging test records—it’s the **final step** of creating a structured report! 📝  

---

### 5️⃣ **HDFS – Storing Final Output**  
- The Reducer’s **processed data** gets stored in **HDFS**, ensuring **distributed and fault-tolerant storage**.  

💡 **Analogy:** Think of uploading a **final exam report** to a central database for long-term storage! 💾  

---

## ⚡ **What About the Combiner?**  
- **If spill files are created**, a **Combiner** can be used **before data reaches the Reducer**.  
- The **Combiner optimizes intermediate data** by **pre-grouping values**, reducing **shuffle overhead**.  
- **Result:** Less **data transfer** → Faster **execution** 🚀  

💡 **Analogy:** Instead of sending **raw student marks** from schools, the teacher **pre-calculates summaries**, making grading **way faster**! 📊  

---

## 🎯 **Why is Reduce-side Combining Important?**  
✅ **Minimizes disk writes** → Improves **storage efficiency**  
✅ **Reduces shuffle data** → Speeds up **Reduce phase execution**  
✅ **Optimizes network transfers** → Boosts **Hadoop performance**  
✅ **Enhances scalability** → Works well for **large datasets**  

---

## 🏁 **Final Thoughts**  
Reduce-side Combining ensures data is **well-organized**, **efficiently processed**, and **optimally stored** in Hadoop. By **reducing redundant transfers**, it makes large-scale data processing **smoother and faster**! 🚀 

---

# 📝 Example of a Combiner – Streamlining Data Processing 🚀  

![image](https://github.com/user-attachments/assets/bdab0d10-fe90-491f-ac6f-16df60093184)  

A **Combiner** is a small yet powerful enhancement in MapReduce, helping **reduce data volume** before shuffling key-value pairs to the **Reducer**. Let's break down this classic Word Count Combiner step by step!  

---

## 📜 **WordCountCombiner Code**
```java
public class WordCountCombiner 
extends Reducer<Text, IntWritable, Text, IntWritable> {
    private IntWritable outputValue = new IntWritable();

    @Override
    protected void reduce(Text key, Iterable<IntWritable> values, Context context)
            throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable count : values) {
            sum += count.get();  // Summing up occurrences
        }
        outputValue.set(sum);
        context.write(key, outputValue);  // Writing reduced output
    }
}
```

---

## 🏗️ **How It Works – Step by Step**  

### 1️⃣ **Summing Values Locally**  
- The **Mapper** outputs key-value pairs like `<word, 1>` multiple times for the same word.  
- Instead of sending **individual occurrences** to the Reducer, the **Combiner groups them locally** first.  

💡 **Analogy:** Imagine counting votes in a large election. Instead of sending **individual votes** to the final counting station, each local booth first **tallies their votes**—this saves a lot of processing time! 🗳️  

---

### 2️⃣ **Local Reduction Before Shuffle**  
- The **reduce method** **iterates over values**, summing them for each word **before sending them to the Reducer**.  
- Only **aggregated counts** are passed forward, reducing **data transfer** between nodes.  

💡 **Analogy:** Instead of delivering raw sales records from every shop, each store **pre-summarizes** daily totals before sending them to headquarters. 📊  

---

### 3️⃣ **Writing Optimized Output**  
- The **combined total** is written out, minimizing **network overhead**.  
- This drastically **reduces the shuffle phase’s workload**, making the **Reducer’s job easier**!  

💡 **Analogy:** Think of summarizing students’ scores before sending them to the school principal. Instead of analyzing **raw marks**, the principal just receives **pre-computed totals** for each subject. 🏫  

---

## 🎯 **Why Use a Combiner?**  
✅ **Optimizes Bandwidth Usage** – Less data transferred between Mapper and Reducer.  
✅ **Enhances Performance** – Faster processing by reducing unnecessary computation.  
✅ **Prevents Redundant Computation** – The Reducer handles **fewer records**, making it more efficient.  

🚀 **End result:** More **scalable** and **optimized** Hadoop workflows!  

---

## 🏁 **Final Thoughts**  
Using a **Combiner** helps **streamline MapReduce operations**, making distributed data processing **more efficient**. The key takeaway: **Reduce before you shuffle!** 🎯  

---

# 🚚 What is a Partitioner in Hadoop MapReduce?  

![image](https://github.com/user-attachments/assets/60309caf-5821-42d4-b28e-c8273aaff03d)  

In **Hadoop MapReduce**, a **Partitioner** is responsible for **determining which Reducer** will process each **key-value pair** from the Mapper’s output. It ensures that **all values associated with the same key are sent to the same Reducer**, enabling correct and efficient data aggregation.

---

## 🔄 **How the Partitioner Works**  

### **1️⃣ Mapper → Partitioner**  
- The **Mapper** generates key-value pairs from the input data.  
- These pairs are then passed to the **Partitioner**, which decides where they should go.  

💡 **Analogy:** Think of a **sorting machine** in a mailroom—it organizes packages so they go to the right recipients! 📦  

---

### **2️⃣ Partitioner → Reducers**  
- The **Partitioner assigns keys to specific Reducers**, ensuring that **all values for the same key are processed together**.  
- Without partitioning, data might be scattered across multiple Reducers, **breaking the logic** of aggregation.  

💡 **Analogy:** Imagine sorting student answers in a school exam—**all answers from the same student must go to the same examiner**, not randomly distributed! 🎓  

---

### **3️⃣ Reducers → NodeManagers**  
- Each **Reducer** processes the assigned data chunks.  
- The **NodeManager** ensures the Reducers execute efficiently within their respective containers.  

💡 **Analogy:** The **exam papers are handed to the right examiners**, ensuring smooth evaluation without confusion! 📜  

---

## 🎯 **Why is Partitioning Important?**  

✅ **Ensures Load Balancing** – Work is evenly distributed across Reducers.  
✅ **Prevents Data Skew** – Avoids overwhelming one Reducer with too much data.  
✅ **Optimizes Parallel Processing** – Allows multiple nodes to process data **simultaneously** for faster results.  

---

# ⚡ Understanding the Default Partitioner  

Hadoop uses the **HashPartitioner** by default, which assigns reducers **based on the hash value of the key**.

### **Default HashPartitioner in Hadoop**  

```java
public class HashPartitioner<K, V> extends Partitioner<K, V> {
    public int getPartition(K key, V value, int numReduceTasks) {
        return (key.hashCode() & Integer.MAX_VALUE) % numReduceTasks;
    }
}
```

### 🔍 **How It Works**  
- **`key.hashCode()`** – Converts the key into a numerical hash.  
- **`& Integer.MAX_VALUE`** – Ensures the hash is **non-negative**.  
- **`% numReduceTasks`** – Distributes the key-value pairs **evenly** across available Reducers.  

💡 **Analogy:** It’s like organizing students alphabetically into exam halls—names starting with **A-C go to Room 1, D-F go to Room 2, etc.** 🎯  

---

# 🛠 **Writing a Custom Partitioner**  

Sometimes, the default **HashPartitioner** might not distribute data optimally. You can create a **Custom Partitioner** based on logic suited to your dataset.

### ✅ **Example: Word Count Partitioner**  

```java
public class WordCountPartitioner extends Partitioner<Text, IntWritable> {
    public int getPartition(Text key, IntWritable value, int numReduceTasks) {
        if (numReduceTasks == 1) {
            return 0;
        }
        return (key.toString().length() * value.get()) % numReduceTasks;
    }
}
```

### 🔍 **How This Custom Partitioner Works**  
- **Uses word length** multiplied by **word frequency** (`value.get()`) to assign Reducers.  
- Applies **modulo operation** (`% numReduceTasks`) to **distribute work evenly**.  

💡 **Example Output (For 3 Reducers)**  

| Word         | Count | `(length * count) % numReduceTasks` | Assigned Reducer |
| ------------ | ----- | ----------------------------------- | ---------------- |
| "data"       | 2     | `(4 * 2) % 3 = 2`                   | Reducer 2        |
| "hadoop"     | 3     | `(6 * 3) % 3 = 0`                   | Reducer 0        |
| "big"        | 1     | `(3 * 1) % 3 = 0`                   | Reducer 0        |
| "processing" | 5     | `(10 * 5) % 3 = 2`                  | Reducer 2        |

🔹 **This prevents data skew and ensures balanced load across Reducers!**  

---

# 🏁 **Final Thoughts**  

Partitioning is **critical** in MapReduce. A well-designed **Partitioner ensures efficient distribution of work**, preventing **bottlenecks** and improving **performance**. Whether using the **default HashPartitioner** or creating a **custom one**, the goal is to **balance Reducer workloads** and **speed up data processing**! 🚀  


---

# 🔄 **Shuffle & Sort in Hadoop MapReduce**  

![image](https://github.com/user-attachments/assets/93372eee-ad72-4d6b-bce2-e15d5be7fcc0)  

The **Shuffle & Sort phase** is one of the most critical stages in **MapReduce**, responsible for efficiently organizing **key-value pairs** before they reach the **Reducer**. Let's break down how it works in simple terms! 🚀  

---

## 🏗️ **Understanding Key-Value Pairs (K2, V2)**  
- **K2 (Keys):** Represent categories such as `"SC"` and `"LA"`.  
- **V2 (Values):** Numerical data linked to the key, such as `(40460, 1), (40061, 1)`.  

💡 **Analogy:** Think of K2 as different **departments**, and V2 as the **transactions** happening within them. For example, `"Sales"` could have multiple daily transactions like `(1000,1), (500,1)`.  

---

## 🔄 **Shuffle & Sort – Step by Step**  

### **1️⃣ Mapper Generates Key-Value Pairs**  
Each **Mapper** processes raw input data and **outputs individual key-value pairs**, such as:  
```plaintext
<SC, (40460, 1)>
<SC, (48847, 1)>
<LA, (35055, 1)>
```
Instead of sending these directly to the **Reducer**, Hadoop optimizes the process using **Shuffle & Sort** first!  

---

### **2️⃣ Sorting Phase – Organizing Data**  
- Keys are **grouped together** so that all values associated with `"SC"` are collected.  
- Example after sorting:  
```plaintext
SC ("40460, 1", "48847, 1", "35055, 1")
```
💡 **Analogy:** Imagine sorting exam papers by subject before grading—this ensures that **all Math papers go to the right teacher**! 📜  

---

### **3️⃣ Combiner Operation – Reducing Intermediate Data**  
- The **Combiner** is applied to optimize **network traffic**, using **commutative and associative operations** to **reduce** the amount of intermediate data sent to the Reducer.  
- Instead of storing each individual count, the **Combiner performs local aggregation**:  
```plaintext
context.write(key, outputValue);
```
💡 **Analogy:** If each student’s **math scores** were individually recorded, it would take too long to process. Instead, **local aggregation** summarizes scores before passing them on! 🏫  

---

### **4️⃣ Reducer Processes Aggregated Data**  
- The **Reducer** takes all the summed values (`sumCount`) and performs the **final computation**:  
```java
outputValue.set(((double) sum)/count);
```
💡 **Analogy:** Instead of grading every quiz separately, the teacher **averages scores for each student** before finalizing the results! 🎯  

---

# 📊 **Checking Shuffle & Sort in YARN Logs**  
Hadoop allows you to **track Shuffle & Sort performance** using YARN logs.  

### ✅ **Fetching Logs for a Specific Application**
```bash
yarn logs -applicationId application_1746198666490_0022
```

💡 **This command retrieves logs** for the Hadoop job, helping debug performance issues.  

![image](https://github.com/user-attachments/assets/dcf55ef3-1817-4859-b7c0-5bd74349031b)

### ✅ **Checking Map Counters in Logs**  
```bash
yarn logs -applicationId application_1746198666490_0022 | grep "MAP counter = "
```
💡 **This helps monitor mapper statistics**, ensuring efficient data flow in the pipeline!  

![image](https://github.com/user-attachments/assets/d6c7e0e5-fddd-4f32-95a8-512304a2b69f)

---

# 🏁 **Final Thoughts**  
The **Shuffle & Sort phase** ensures that data is **organized efficiently**, reducing **network congestion** and speeding up **parallel processing** in Hadoop. The **Combiner** further optimizes performance by **aggregating values locally** before they reach the Reducer! 🚀  

---

# 🚀 Partition Continued – Understanding Hadoop Data Flow  

![image](https://github.com/user-attachments/assets/2e3926e6-2868-455e-9753-91c549ecc05b)  

The **partitioning process in Hadoop MapReduce** is essential for **efficient data distribution and processing**. This data flow diagram highlights how raw data transitions **step by step** before reaching meaningful output. Let’s dive in!  

---

## 📌 **Step-by-Step Breakdown of Hadoop MapReduce Data Flow**  

### **1️⃣ Input Splits from HDFS**  
- The data stored in **HDFS** is **divided** into smaller pieces called **input splits**.  
- These splits allow **parallel processing** for efficiency.  

💡 **Analogy:** Imagine dividing a **big book** into separate chapters so different people can read parts simultaneously! 📖  

---

### **2️⃣ InputFormat – Converting Data into Key-Value Pairs**  
- The **InputFormat** defines how each split is structured into **<key, value> pairs**, making data ready for the **Mapper**.  
- Different formats suit different types of data sources.  

💡 **Analogy:** Think of a **translator** converting a book into different languages based on the reader’s needs! 📚  

---

### **3️⃣ Mapper Execution – Processing Key-Value Pairs**  
- The **Mapper** processes each key-value pair independently.  
- It applies **transformations, filtering, and local aggregations** before passing results forward.  

💡 **Analogy:** A **chef** preparing individual meal components before assembling the final dish! 🍽️  

---

### **4️⃣ Reducer Execution – Final Processing**  
- The output from Mappers is **shuffled, sorted, and grouped**, allowing the **Reducer** to consolidate results.  
- This step ensures meaningful **data aggregation** based on keys.  

💡 **Analogy:** A **final report** being compiled after receiving categorized survey responses from multiple locations! 📝  

---

### **5️⃣ OutputFormat – Structuring the Final Storage**  
- The processed results are **formatted properly** before being stored in **HDFS**.  
- The chosen **OutputFormat** determines how the results appear for further use.  

💡 **Analogy:** Formatting a **report neatly** before submitting it to management! 📊  

---

# 📂 **Built-in Hadoop Input Formats**  

Hadoop provides **various built-in InputFormats** to structure raw data efficiently. Here's a quick rundown:  

### ✅ **FileInputFormat<K, V>**  
- Acts as the **parent class** for most input formats.  
- Reads data from HDFS and splits it into **InputSplits** for parallel execution.  

---

### ✅ **TextInputFormat<LongWritable, Text>** _(Default)_  
- Processes **text files line by line**, treating:  
  - `LongWritable` → Line offset as the key  
  - `Text` → The line content as the value  
- Ideal for **log files and structured text data**.  

---

### ✅ **SequenceFileInputFormat<K, V>**  
- Works with **binary files** using Hadoop’s SequenceFile format.  
- Great for storing **compressed and efficiently retrievable** data.  

---

### ✅ **KeyValueTextInputFormat<Text, Text>**  
- Reads text data as **key-value pairs** where:  
  - The **first token** is the key  
  - The remaining line is the value  
- Perfect for structured records where key-based grouping is required.  

---

### ✅ **CombineFileInputFormat<K, V>**  
- Designed for **handling many small files efficiently**.  
- Combines multiple tiny files into **larger splits**, reducing overhead.  

---

### ✅ **MultipleInputs**  
- Allows **different InputFormats** for various datasets in a single job.  
- Useful for **mixing data types** (XML, CSV, JSON, etc.).  

---

# 📤 **Built-in Hadoop Output Formats**  

Once the **Reducer** finishes processing, data needs to be written **in a structured format** to storage. Here’s how Hadoop handles output formatting:  

### ✅ **FileOutputFormat<K, V>**  
- Serves as the **parent class** for all output formats.  
- Sends processed data to **HDFS** in a structured way.  

---

### ✅ **TextOutputFormat<K, V>** _(Default)_  
- Saves data in **plain text** with a separator between keys and values.  
- Best suited for **human-readable outputs**.  

---

### ✅ **SequenceFileOutputFormat<K, V>**  
- Writes output as **binary Hadoop SequenceFile format**.  
- Excellent for **efficient storage & retrieval of large datasets**.  

---

### ✅ **MultipleOutputs<K, V>**  
- Allows **writing results to multiple destinations** within a job.  
- Ideal for cases where output needs **segmentation per category or format**.  

---

### ✅ **NullOutputFormat<K, V>**  
- Used when **no output is required**.  
- Beneficial for **debugging or testing** jobs without generating actual results.  

---

### ✅ **LazyOutputFormat<K, V>**  
- Writes output **only when a reducer generates non-empty results**.  
- Avoids **creating unnecessary empty files** in HDFS.  

---

# 🏁 **Final Thoughts**  

Partitioning is **essential** for efficient **data flow, parallel processing, and load balancing** in Hadoop. Choosing the right **InputFormat and OutputFormat** ensures **optimized performance** for large-scale data applications! 🚀  

---

# 🚀 Optimizing MapReduce Jobs – Best Practices for High Performance  

Optimizing Hadoop **MapReduce jobs** is essential for **improving efficiency, reducing computational overhead, and ensuring smooth execution** of large-scale data processing. Here’s a refined breakdown of **key optimization strategies!** 🔥  

---

## 🔄 **1️⃣ Distribute Workload Evenly Across NodeManagers**  
- Tasks should be **balanced** across available nodes.  
- **Custom partitioners** help distribute data evenly, preventing one node from getting overloaded.  

💡 **Analogy:** Imagine a classroom with **group projects**—spreading work evenly ensures everyone contributes equally rather than one student doing it all! 📚  

---

## 🔧 **2️⃣ Use a Combiner to Reduce Shuffle Overhead**  
- The **Combiner** minimizes **data transfer** between the Mapper and Reducer.  
- Essential for **aggregations** like sum and count, reducing unnecessary computation.  

💡 **Analogy:** Instead of counting individual votes at the **national level**, each district **first summarizes local votes**, reducing workload before final tabulation! 🗳️  

---

## 🏗️ **3️⃣ Avoid Instantiating New Objects**  
- **Creating new objects** inside loops increases **garbage collection overhead**.  
- **Reuse existing objects** whenever possible to save memory.  

💡 **Tip:** Instead of declaring new `IntWritable` inside a loop, **reuse one instance**, updating its value dynamically.  

---

## 🚀 **4️⃣ Use StringBuilder Instead of String Concatenation**  
- Strings are **immutable**—every modification creates a **new object**, increasing memory usage.  
- **StringBuilder** optimizes string operations by modifying existing memory instead of creating new instances.  

💡 **Example:** Instead of this ⛔:  
```java
String result = "";
for (String value : values) {
    result += value;
}
```
Use this ✅:  
```java
StringBuilder result = new StringBuilder();
for (String value : values) {
    result.append(value);
}
```
**Outcome:** Less memory allocation, faster execution! 🚀  

---

## 🗜️ **5️⃣ Enable Data Compression to Reduce Disk I/O**  
- Use **SequenceFile compression**, **Snappy**, or **Gzip** for **intermediate Mapper output and final Reducer output**.  
- Reduces **storage footprint** and speeds up data transfers.  

💡 **Tip:**  
```java
job.setOutputFormatClass(SequenceFileOutputFormat.class);
SequenceFileOutputFormat.setOutputCompressionType(job, CompressionType.BLOCK);
```
**Result:** Faster processing due to reduced file sizes!  

---

## 🔢 **6️⃣ Store Numbers in Binary Format Instead of Text**  
- Numbers in **text format** take **more space** and slow down processing.  
- Using **binary representations** saves space and speeds up computation.  

💡 **Tip:** Instead of storing `"100"` as text, **use binary storage** for efficiency.  

---

## 🎯 **7️⃣ Define and Configure a RawComparator for Faster Sorting**  
- **RawComparators** speed up **sorting** by comparing **binary representations directly**, reducing deserialization overhead.  
- Instead of converting objects to Java types, it works on raw bytes.  

💡 **Example of a RawComparator:**  
```java
public class MyRawComparator extends WritableComparator {
    protected MyRawComparator() {
        super(Text.class);
    }
    @Override
    public int compare(byte[] b1, int s1, int l1, byte[] b2, int s2, int l2) {
        return WritableComparator.compareBytes(b1, s1, l1, b2, s2, l2);
    }
}
```
🚀 **Result:** Sorting becomes significantly **faster**, improving job execution!  

---

## 🔍 **8️⃣ Use StringUtils.split Instead of String.split for Faster Parsing**  
- `String.split()` relies on **regex-based parsing**, which is **slower**.  
- **StringUtils.split()** is **optimized** for faster text processing.  

💡 **Example Comparison:**  
⛔ Using `String.split()` (slower):  
```java
String[] words = line.split(" ");
```
✅ Using `StringUtils.split()` (faster):  
```java
String[] words = StringUtils.split(line, ' ');
```
🚀 **Outcome:** Faster parsing, reduced overhead!  

---

# 🔥 **Why Doesn't Hadoop Use Java's Primitive Datatypes?**  
Although Hadoop is **built on Java**, it doesn’t use **primitive datatypes** (`int`, `double`, etc.). Here’s why:  

### 🏗️ **1️⃣ Hadoop is Fully Object-Oriented**  
- Java uses **primitive datatypes**, but Hadoop is **designed for handling complex objects**.  

---

### 🔄 **2️⃣ Serialization – The Key Factor**  
- Hadoop relies on **serialization** to **store, process, and transfer data efficiently**.  
- Java primitives like `int` and `double` **aren't serializable**, but Hadoop’s **Writable classes** (`IntWritable`, `DoubleWritable`) **are**.  

💡 **Example:**  
⛔ **Using Java primitives (Not Serializable)**
```java
int num = 100;  // Not ideal for Hadoop serialization
```
✅ **Using Hadoop’s Writable types (Serializable)**
```java
IntWritable num = new IntWritable(100);  // Optimized for Hadoop processing
```
🚀 **Result:** Proper serialization, making distributed processing more efficient!  

---

# 🏁 **Final Thoughts**  
Optimizing Hadoop **MapReduce jobs** leads to **better performance, reduced processing time, and enhanced scalability**.  

💡 **Key Takeaways:**  
✅ **Use Combiners** to **minimize shuffle** overhead.  
✅ **Enable compression** for **faster data transfers**.  
✅ **Avoid unnecessary object creation** to **reduce memory usage**.  
✅ **Optimize sorting with RawComparators**.  
✅ **Use Hadoop’s Writable datatypes** instead of Java primitives.  

---

# 🗜️ Data Compression in Hadoop 🚀  

Data compression in Hadoop plays a **critical role** in **reducing storage requirements, improving processing speed, and optimizing network bandwidth**. Different compression codecs help **efficiently manage large-scale data**, minimizing I/O overhead.  

---

## 🔧 **Why Use Data Compression?**  
✅ **Reduces Storage Usage** – Compressed files occupy **less disk space**.  
✅ **Speeds Up Processing** – Less data means **faster reads/writes**.  
✅ **Optimizes Network Transfer** – Compressed data reduces **shuffling costs**.  
✅ **Enhances Performance in Distributed Systems** – Hadoop jobs **run faster** due to minimized file sizes.  

---

## 🏗️ **Common Compression Codecs Used in Hadoop**  

### 🚀 **1️⃣ Snappy (Fast & Lightweight)**  
- **Codec:** `org.apache.hadoop.io.compress.SnappyCodec`  
- **Best For:** **High-speed** compression/decompression with **moderate space savings**.  
- **Advantages:**  
  - ✅ **Super fast**, optimized for performance.  
  - ✅ Works well for real-time applications requiring quick I/O.  
- **Limitations:**  
  - ❌ Not the most **space-efficient** compared to other methods.  

💡 **Analogy:** Think of Snappy like a **zippered backpack**—quick to open/close but doesn’t shrink content much! 🎒  

---

### 🗜️ **2️⃣ Gzip (Strong Compression & Widely Used)**  
- **Codec:** `org.apache.hadoop.io.compress.GzipCodec`  
- **Best For:** Achieving **high compression** ratios, suitable for storing large files.  
- **Advantages:**  
  - ✅ **Widely supported**, useful for archival data.  
  - ✅ **Good compression ratio** for space efficiency.  
- **Limitations:**  
  - ❌ **Slower decompression** than Snappy.  
  - ❌ **Not splittable**, meaning files can’t be divided easily for parallel processing.  

💡 **Analogy:** Think of Gzip as **vacuum-sealed bags**—compact but slower to unpack! 👜  

---

### 🔄 **3️⃣ Bzip2 (High Compression, Splittable)**  
- **Codec:** `org.apache.hadoop.io.compress.BZip2Codec`  
- **Best For:** **Efficiently compressing large files** while remaining **splittable**, making it Hadoop-friendly.  
- **Advantages:**  
  - ✅ **Splittable**, meaning Hadoop can process chunks of compressed files in parallel.  
  - ✅ **Higher compression ratio** than Gzip.  
- **Limitations:**  
  - ❌ **Slower compression/decompression** compared to Snappy & Gzip.  

💡 **Analogy:** Think of Bzip2 like **efficient luggage packing**—takes longer, but saves space! 🧳  

---

### 🔄 **4️⃣ LZO (Splittable & Optimized for Speed)**  
- **Codec:** `com.hadoop.compression.lzo.LzopCodec`  
- **Best For:** **Balancing speed and compression ratio**, often used for **large-scale log files**.  
- **Advantages:**  
  - ✅ **Splittable**, great for Hadoop’s distributed processing.  
  - ✅ **Fast decompression**, making data retrieval smoother.  
- **Limitations:**  
  - ❌ **Lower compression ratio** compared to Bzip2 or Gzip.  

💡 **Analogy:** Think of LZO like a **roll-up bag**—good balance between space and speed! 🎒  

---

### 🏗️ **5️⃣ DEFLATE (Versatile & Balanced Compression)**  
- **Codec:** `org.apache.hadoop.io.compress.DefaultCodec`  
- **Best For:** **General-purpose compression**, balancing **speed and storage efficiency**.  
- **Advantages:**  
  - ✅ **Well-optimized**, commonly used in Hadoop.  
  - ✅ Works well across different types of data.  
- **Limitations:**  
  - ❌ **Not specialized** for any one particular use case.  

💡 **Analogy:** Think of DEFLATE as **a hybrid suitcase**—flexible but not the best in either compression or speed! 🛄  

---

# 🔥 **Choosing the Right Compression Codec**  

| **Codec**  | **Best For**  | **Splittable?** | **Compression Strength** | **Speed** |
|------------|--------------|----------------|------------------|------------|
| **Snappy** | Fast processing | ❌ No  | 🔵 Moderate | 🟢 High |
| **Gzip** | Archival data | ❌ No | 🔴 High | 🔴 Slow |
| **Bzip2** | Large files, Hadoop-friendly | ✅ Yes | 🟢 High | 🔴 Slow |
| **LZO** | Large-scale logs | ✅ Yes | 🔵 Moderate | 🟢 Fast |
| **DEFLATE** | General compression | ❌ No | 🔵 Moderate | 🔵 Medium |

---

# 🏁 **Final Thoughts**  

Compression **enhances storage efficiency and speeds up Hadoop jobs**, making **data movement faster and cheaper**. Choosing the right codec **depends on the use case**—whether prioritizing **speed, compression strength, or splittability**.  

---

# 🚨 Limitations of Compression – Balancing Performance & Efficiency  

Data compression **enhances storage efficiency and speeds up Hadoop workflows**, but it comes with trade-offs. Let’s explore the **key limitations** that impact decision-making in **big data environments**!  

---

## ⚖️ **1️⃣ Space vs. Time Trade-off**  
- Compression **reduces file size**, saving **disk space** and **network bandwidth**.  
- However, **compressing & decompressing** data **adds extra computational time**.  

💡 **Key Question:**  
Is the **time cost** of compression worth the **storage savings**?  

### ✅ **Scenario Where Compression Helps**  
- If the **dataset is massive**, compression **reduces storage needs** and **speeds up transfers**.  
- Example: **Log files in Hadoop** → Smaller **compressed logs** minimize I/O overhead.  

### ❌ **Scenario Where Compression Hurts**  
- If the **data needs frequent access**, decompression **adds unnecessary delays**.  
- Example: **Real-time streaming analytics** → Compression might **slow down** data retrieval.  

💡 **Analogy:** Imagine stuffing clothes into a **vacuum-sealed bag**. It **saves space**, but you need **extra time** to unpack it when needed! 🧳  

---

## 📝 **2️⃣ Splittable vs. Non-Splittable Compression Formats**  
One of the biggest concerns in Hadoop **MapReduce** is whether a **compressed file can be split into chunks** for **parallel processing**.  

### ✅ **Splittable Compression Formats** (Good for Hadoop)  
| **Compression Format** | **Splittable?** | **Best Use Case** |
|------------------------|----------------|-------------------|
| **Bzip2** | ✅ Yes | Large datasets needing parallel processing |
| **LZO** | ✅ Yes | Distributed logs and transactional data |

💡 **Why Splittable Matters?**  
Hadoop **divides large files** into smaller chunks for **parallel execution**. If compression **prevents splitting**, only **one node** processes the file, defeating Hadoop’s **distributed architecture**!  

---

### ❌ **Non-Splittable Compression Formats** (Can Slow Down Hadoop)  
| **Compression Format** | **Splittable?** | **Best Use Case** |
|------------------------|----------------|-------------------|
| **Gzip** | ❌ No | Archival data where splitting isn’t needed |
| **Snappy** | ❌ No | Real-time applications requiring fast I/O |
| **DEFLATE** | ❌ No | General-purpose compression |

💡 **Problem With Non-Splittable Compression**  
- If a **large Gzip file** is stored, **one reducer** processes it instead of **multiple parallel reducers**.  
- This slows down Hadoop jobs by **forcing sequential execution** rather than parallel computing.  

💡 **Analogy:** Imagine scanning a **massive book** for keywords. If you **can't divide the pages**, you must **scan everything manually** rather than having multiple people help! 📚  

---

## 🏁 **Final Thoughts**  
Choosing the right compression format **depends on the use case**! 🚀  

✅ **If processing large datasets in Hadoop → Use splittable formats (Bzip2, LZO).**  
✅ **If storing data for archival purposes → Use non-splittable formats (Gzip, Snappy).**  
✅ **If optimizing speed over compression → Choose Snappy or LZO for high-speed applications.**  

---

# 🔬 **Lab 6: Configuring Compression in Hadoop MapReduce**  

In **BigDataVM's IdeaIntelliJ**, **SnappyCodec** wasn’t working, so we switched to **BZip2Codec** for **compressing Mapper output and final Reducer output** in Hadoop MapReduce jobs.  

---

## ⚙️ **Compression Configuration in Hadoop**  

### ✅ **Enabling Compression for Mapper Output**  
```java
conf.setBoolean(MRJobConfig.MAP_OUTPUT_COMPRESS, true);
// conf.setClass(MRJobConfig.MAP_OUTPUT_COMPRESS_CODEC, SnappyCodec.class, CompressionCodec.class);
conf.setClass(MRJobConfig.MAP_OUTPUT_COMPRESS_CODEC, org.apache.hadoop.io.compress.BZip2Codec.class, CompressionCodec.class);
```
🔹 **Purpose:** Reduces network overhead by compressing Mapper output before shuffling.  

---

### ✅ **Enabling Compression for Final Reducer Output**  
```java
conf.setBoolean(FileOutputFormat.COMPRESS, true);
// conf.setClass(FileOutputFormat.COMPRESS_CODEC, SnappyCodec.class, CompressionCodec.class);
conf.setClass(FileOutputFormat.COMPRESS_CODEC, org.apache.hadoop.io.compress.BZip2Codec.class, CompressionCodec.class);
```
🔹 **Purpose:** Saves HDFS storage space by writing compressed reducer output files (`part-r-00000`).  

---

## ⚠️ **What Happens If We Remove Compression Configuration?**  

If we **remove this part of code** and run the Hadoop job via **YARN**, the output **will be different** in key ways:  

### 🔴 **1️⃣ No Compression for Mapper Output**  
- **Higher network I/O overhead** during the shuffle phase.  
- **Increased data transfer between nodes**, slowing down execution time.  

💡 **Example:** Without compression, Mapper output increases **network congestion** like sending **raw images** instead of compressed ones! 🖼️  

---

### 🔴 **2️⃣ No Compression for Final Reducer Output**  
- **Larger storage footprint** in HDFS.  
- Output files (`part-r-00000`) **will not be compressed**, making them **heavier**.  

💡 **Example:** It’s like storing **uncompressed high-resolution videos**—it takes up more space! 🎥  

---

## 🎯 **Key Takeaways**  
✅ **Compression Reduces Shuffle & Storage Overhead** – Makes Hadoop jobs **faster & efficient**.  
✅ **BZip2Codec is Splittable** – Unlike Snappy & Gzip, BZip2 allows **parallel processing**.  
✅ **Removing Compression Increases File Size** – HDFS storage consumption grows.

---

### 📜 Can We Perform MapReduce Without Using Java? Can We Use Python?

Yes, you **can** perform MapReduce without using Java! This is done using a concept called **Hadoop Streaming**. 

#### 🔍 What is Hadoop Streaming?
Hadoop Streaming is a utility that allows you to **run MapReduce jobs with any programming language**. Instead of writing Mappers and Reducers in Java, you can use **Python, R, shell scripts, or even other executables**.

💡 **Example**:  
Imagine you have a text file containing names, and you want to count how often each name appears. Using **Hadoop Streaming**, you can:
- Write a **Python script** as the Mapper to process input data.
- Write another **Python script** as the Reducer to aggregate the results.

---

### 🚫 Why Do Many People Not Use Hadoop Streaming?

Even though Hadoop Streaming allows non-Java languages for MapReduce, it is **not widely used** for a few reasons:

1️⃣ **Apache Spark Was Introduced**  
   - Apache Spark is **faster** and more efficient for processing large-scale data.  
   - Unlike traditional MapReduce, Spark operates in-memory, reducing disk I/O operations.  
   - It supports **high-level APIs** in Python, Java, Scala, and R, making it much easier to work with than Hadoop Streaming.

2️⃣ **MapReduce’s Native Implementation is in Java**  
   - Hadoop’s MapReduce engine is designed to **work best with Java**.  
   - Java-based MapReduce jobs perform better because they **directly integrate** with the Hadoop ecosystem.  
   - Using Python or other languages via Hadoop Streaming adds a slight performance overhead.

3️⃣ **Spark Supports Multiple Languages**  
   - Spark allows programming in **Python, R, Java, and Scala**, which makes it **more flexible** than Hadoop Streaming.  
   - Python users prefer **PySpark**, which is a **more efficient** way of writing distributed processing jobs than using Hadoop Streaming.  
   
---

### 🖼️ Image Description: Hadoop Streaming Flow

![image](https://github.com/user-attachments/assets/78fe4217-78fd-4efd-a3cb-b54daa816e1c)

The image explains **how Hadoop Streaming works**:

1️⃣ **Input Split** → The input data is broken into pieces and formatted as `<key1, value1>` pairs.  
2️⃣ **Mapper (External Script)** → Converts `<key1, value1>` into lines of text and **sends them to an external program** (e.g., Python script).  
3️⃣ **Python Mapper Script** → Processes stdin (input) and **outputs `<key2, value2>` pairs**.  
4️⃣ **Reducer (External Script)** → Receives `<key2, (value2, value2, …)>` and processes them via another external program.  
5️⃣ **Python Reducer Script** → Outputs final `<key3, value3>` pairs as the result.  

💡 **This image helps visualize how non-Java languages interact with Hadoop Streaming!**

---

### 🚀 Running a Hadoop Streaming Job

A **Streaming Job** is just like a traditional **MapReduce Job**, except it **does not require Java-based Mappers and Reducers**. Instead, it allows using **any executable script** (like Python, Shell, or Perl).

#### 🏗️ Command Structure:
To run a Hadoop Streaming job, we use the **hadoop-streaming.jar** file:

```bash
hadoop jar $HADOOP_HOME/lib/hadoop-streaming.jar \
-input <input_directories> \
-output <output_directories> \
-mapper <mapper_script> \
-reducer <reducer_script>
```

### 🛠️ Breakdown of the Command:
🔹 **hadoop jar $HADOOP_HOME/lib/hadoop-streaming.jar** → Runs the Hadoop Streaming utility.  
🔹 **-input input_directories** → Specifies the HDFS directory containing input files.  
🔹 **-output output_directories** → Specifies the HDFS directory where output will be saved.  
🔹 **-mapper mapper_script** → Defines the script to process input (Python, Shell, etc.).  
🔹 **-reducer reducer_script** → Defines the script to aggregate/compute results.

💡 **Example for Python MapReduce:**  
Imagine you have a large dataset containing words and want to **count word occurrences** using Python.

#### 🎯 Python Mapper (`mapper.py`)
```python
import sys
for line in sys.stdin:
    words = line.strip().split()
    for word in words:
        print(f"{word}\t1")  # Output as key-value pairs (word, 1)
```

#### 📝 Python Reducer (`reducer.py`)
```python
import sys
from collections import defaultdict

word_counts = defaultdict(int)
for line in sys.stdin:
    word, count = line.strip().split("\t")
    word_counts[word] += int(count)

for word, count in word_counts.items():
    print(f"{word}\t{count}")  # Output as key-value pairs (word, total count)
```

🔹 **Executing the Job:**
```bash
hadoop jar $HADOOP_HOME/lib/hadoop-streaming.jar \
-input /user/hadoop/input \
-output /user/hadoop/output \
-mapper mapper.py \
-reducer reducer.py
```

✨ This command runs a MapReduce job **without Java**, using Python for both **Mapper** and **Reducer**.

---
