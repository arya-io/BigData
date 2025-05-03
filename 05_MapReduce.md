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

## 🚚 **What is a Partitioner?**

![image](https://github.com/user-attachments/assets/60309caf-5821-42d4-b28e-c8273aaff03d)

This diagram explains the role of the **Partitioner** in a data processing framework, likely **Hadoop MapReduce**.

### **What is a Partitioner?**

* The **Partitioner** decides how the **Mapper’s output key-value pairs** are distributed to the **Reducers**.
* It ensures that all values for the same key are processed by the same **Reducer**, enabling efficient and accurate data aggregation.

### **Key Elements in the Diagram:**

1. **Mapper → Partitioner**

   * The **Mapper** processes data and generates key-value pairs.
   * These key-value pairs are passed to the **Partitioner** for distribution.

2. **Partitioner → Reducers**

   * The **Partitioner** determines which **Reducer** receives which key-value pairs, ensuring that values associated with the same key are grouped together.

3. **Reducers → NodeManagers**

   * Each **Reducer** operates on a **NodeManager**, which manages the execution of the tasks in containers.
   * Reducers process their assigned data chunks, aggregating values for each key.

### **Why is a Partitioner Important?**

* **Load Balancing**: Ensures that work is evenly distributed across the reducers.
* **Avoids Data Skew**: Prevents one reducer from being overloaded with too much data, improving performance.
* **Parallel Processing**: Ensures that data can be processed in parallel across multiple nodes for faster results.

---

### **Step-by-Step Breakdown of the Partitioning Process in Hadoop:**

1. **Mapper Outputs `<key, value>` Pairs**

   * The **Mapper** processes the input data and generates key-value pairs that hold the meaningful data.

2. **Data is Passed to the Partitioner**

   * The **Partitioner** determines which **Reducer** should receive each key-value pair.
   * It ensures that values for the same key go to the same **Reducer**.

3. **Partitioner Assigns Reducer Using `getPartition` Method**

   * The `getPartition` method calculates an integer between 0 and (number of Reducers - 1), deciding which **Reducer** gets each key-value pair.
   * For example, if there are **3 Reducers**, `getPartition` may return **0**, **1**, or **2**, mapping key-value pairs to corresponding Reducers.

4. **Reducers Process Assigned Data**

   * Each **Reducer** processes the key-value pairs it has been assigned, ensuring that the processing is done efficiently and in parallel.

### **Why is Partitioning Important?**

* **Ensures Load Balancing**: Guarantees an even distribution of work across Reducers.
* **Prevents Data Skew**: Helps avoid situations where a Reducer gets too much data while others get too little.
* **Optimizes Performance**: By ensuring even data distribution, partitioning speeds up parallel data processing, thus enhancing performance.

---

## 📦 **The Default Partitioner**

```java
public class HashPartitioner<K, V> extends Partitioner<K, V> {
    public int getPartition(K key, V value, int numReduceTasks) {
        return (key.hashCode() & Integer.MAX_VALUE) % numReduceTasks;
    }
}
```

### **Explanation:**

* The **`HashPartitioner`** is the default partitioner used in Hadoop MapReduce.
* It uses the **`hashCode()`** method of the key to determine the partition. The partition is computed by performing the following steps:

  * **`key.hashCode()`** → Generates a hash value for the key.
  * **`& Integer.MAX_VALUE`** → Ensures the hash value is non-negative.
  * **`% numReduceTasks`** → Distributes the data evenly across the available reducers based on the number of reducers (`numReduceTasks`).

---

## 🛠️ **Writing a Custom Partitioner**

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

### **Explanation of Custom Partitioner:**

* The **`WordCountPartitioner`** is a **custom partitioner** designed for the **WordCount** application in Hadoop's MapReduce framework.
* It extends the **`Partitioner<Text, IntWritable>`**, which is the default Partitioner type for key-value pairs where the key is of type `Text` (string) and the value is of type `IntWritable` (integer).

#### **Key Components of the Code:**

1. **Extends `Partitioner<Text, IntWritable>`:**

   * The custom partitioner extends Hadoop’s base **Partitioner** class, allowing the developer to specify custom logic for partitioning.

2. **`getPartition()` Method:**

   * This method accepts:

     * **`Text key`**: The word being counted (for instance, `"data"`).
     * **`IntWritable value`**: The count of occurrences of the word (for example, `2` for `"data"`).
     * **`int numReduceTasks`**: The number of reducers available for the job.
   * The method defines the partitioning logic:

     * If there is only **one Reducer** (`numReduceTasks == 1`), all data is sent to **Reducer 0**.
     * Otherwise, the logic for partitioning is based on **`(key.length() * value.get()) % numReduceTasks`**.

       * This formula uses the length of the word (`key.toString().length()`) multiplied by the frequency of the word (`value.get()`), and then applies a modulo operation to determine which reducer the key-value pair should go to.

### **Partitioning Logic Example:**

#### **Scenario: `numReduceTasks = 3`**

| Word         | Count | `(length * count) % numReduceTasks` | Partition Assigned |
| ------------ | ----- | ----------------------------------- | ------------------ |
| "data"       | 2     | `(4 * 2) % 3 = 2`                   | Reducer 2          |
| "hadoop"     | 3     | `(6 * 3) % 3 = 0`                   | Reducer 0          |
| "big"        | 1     | `(3 * 1) % 3 = 0`                   | Reducer 0          |
| "processing" | 5     | `(10 * 5) % 3 = 2`                  | Reducer 2          |

#### **Why Use a Custom Partitioner?**

* **Even Load Distribution**: Custom partitioning can ensure that the data is more evenly distributed across reducers, leading to better resource utilization.
* **Improved Performance**: By customizing the partitioning logic, you can avoid **data skew**, where some reducers receive much larger amounts of data than others, which can lead to slower processing times.
* **Optimization Based on Specific Relationships**: The custom logic might consider specific relationships in the key-value pairs (such as word length and count) to improve the distribution of data based on the application’s needs.

---

### **Integrating the Custom Partitioner into a WordCountJob**

To use the `WordCountPartitioner` in your **WordCountJob**, you should include it as an inner class within your existing WordCount application. Afterward, follow these steps:

1. **Include the Custom Partitioner as an Inner Class:**

   * Add the `WordCountPartitioner` class to the WordCount job file.

2. **Create a JAR File:**

   * Compile your project and package it into a **JAR file**.

3. **Execute the WordCount Job:**

   * Submit the job to the Hadoop cluster using the `hadoop jar` command.

   Example command:

   ```bash
   hadoop jar wordcount.jar org.apache.hadoop.examples.WordCount input output
   ```

This process will ensure that the custom partitioning logic is applied, optimizing the distribution of work across the reducers.

---

This section explains how you can customize the default **Partitioner** in Hadoop MapReduce to suit your specific application needs.
