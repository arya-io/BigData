# MapReduce

MapReduce is a ETL Framework where program is written.

Map Phase: Colleect data
Shuffle/Sort
Reduce Phase

![image](https://github.com/user-attachments/assets/f2265f8c-0ced-458c-840f-0466a63eee60)

---

## Understanding Map Reduce

1. Suppose a file is the input to a MapReduce job.
That file is broken down into blocks stored on
DataNodes across the Hadoop cluster.

![image](https://github.com/user-attachments/assets/0036978e-cc30-4158-aa68-841ceaf24453)

2. During the Map phase, map tasks process the
input of the MapReduce job, with a map task
assigned to each Input Split. The map tasks are
Java processes that ideally run on the
DataNodes where the blocks are stored.

3. Each map task processes its Input Split and outputs
records of <key, value> pairs.

![image](https://github.com/user-attachments/assets/9b66e4a2-9418-4e5d-8efc-54a500d02986)

4. The <key,value> pairs go through a shuffle/sort phase, where records with the
same key end up at the same reducer. The specific pairs sent to a reducer
are sorted by key, and the values are aggregated into a collection.

5. Reduce tasks run on a NodeManager as a Java process. Each Reducer
processes its input and outputs <key,value> pairs that are typically written to
a file in HDFS.

![image](https://github.com/user-attachments/assets/520418aa-23ac-4080-84eb-066b6819a359)

---

## The Key/Value Pairs of MapReduce

![image](https://github.com/user-attachments/assets/9bbb4c7f-6a61-4556-92ea-6f10664421c2)

---

## WordCount in MapReduce

This is one of the use case of MapReduce

![image](https://github.com/user-attachments/assets/a0ddf7c1-8d50-4639-8f9f-537d10f3e147)

The input file can be of any size (MB, GB, TB, PB, etc.)

Step 1: The mappers read the file's blocks from HDFS line-by-line.
Step 2: The lines of text are split into words and output to the reducer.
Step 3: The shuffle/sort phase combines pairs with the same key.
Step 4: The reducers add up the "1's" and output the word and its count.

---

## Demonstration: Understanding MapReduce

yarn jar /usr/hdp/2.6.0.3-8
![image](https://github.com/user-attachments/assets/5aa07f74-7737-46d1-be89-93fabb655804)


executing the jar file:
![image](https://github.com/user-attachments/assets/d010f6b8-9f8a-4f81-8b34-35df6f6b4b65)
![image](https://github.com/user-attachments/assets/950d4c01-7e37-4911-9608-b0f6428c551f)

hdfs dfs -ls wordcount_output
![image](https://github.com/user-attachments/assets/19eeeeda-431a-4b64-a96e-2cc7c6086ad9)

hdfs dfs -cat wordcount_output/part-r-00000
![image](https://github.com/user-attachments/assets/8271a8d3-2524-458a-84d2-53f8bc2646b3)

---

Now, we are performing the same MapReduce task on BigDataVM:

yarn jar ~/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount -D mapred.reduce.tasks=2 constitution.txt wordcount_output

![image](https://github.com/user-attachments/assets/60f7b43b-6f85-46a9-9cb8-02deb32e7936)

![image](https://github.com/user-attachments/assets/a2bd032d-185e-4971-b2f9-37539344a513)

![image](https://github.com/user-attachments/assets/774f7378-2f92-41bc-99bb-22f81e819265)

What is a .jar file?
A .jar (Java ARchive) file is a package format used in Java to distribute a collection of Java classes, metadata, and resources (like images or property files) into a single compressed file. It’s essentially a ZIP file with a .jar extension, designed for Java applications.

We merged the files present in wordcount_output to /tmp/final_op, using command:
hdfs dfs -getmerge wordcount_output /tmp/final_op
![image](https://github.com/user-attachments/assets/a7444982-4838-4c6a-9f1a-d99513890575)
![image](https://github.com/user-attachments/assets/54483b22-c30d-432a-9c63-b83b8d36e8ea)

Showing line count and word count of final_op:
talentum@talentum-virtual-machine:/tmp$ wc -l final_op
1683 final_op
talentum@talentum-virtual-machine:/tmp$ wc final_op
 1683  3366 17049 final_op
![image](https://github.com/user-attachments/assets/201642ac-fc14-47c6-8eb6-24fa54b558e5)

---

WordCountMapper:

Explain this code:

```java
public class WordCountMapper
extends Mapper<LongWritable, Text, Text, IntWritable> { // This is generic

@Override

protected void map(LongWritable key, Text value,

Context context)

throws IOException, InterruptedException {
String currentLine = value.toString();
String [] words = currentLine.split(" ");
for(String word : words) {
Text outputKey = new Text(word);
context.write(outputKey, new IntWritable(1));
}
}

}
```

If we have to extend the Mapper generic, we must override the map method.
Text, IntWritable: This is treated as K1, V1.
Java does not have LongWritable, Text and IntWritable datatypes.
Those are of Hadoop's.
Context is responsible for generating K2, V2 pairs.

This `WordCountMapper.java` class is a part of a Hadoop MapReduce program for counting word occurrences in a dataset. It extends the `Mapper` class, which processes input key-value pairs and generates intermediate key-value pairs for the reducer.

### Explanation of the Code:
1. **Class Definition**  
   ```java
   public class WordCountMapper extends Mapper<LongWritable, Text, Text, IntWritable>
   ```
   - It extends the `Mapper` class with generic types:
     - `LongWritable`: Represents the offset (byte position) of the line in the file.
     - `Text`: Represents the line of text being processed.
     - `Text`: The key for the output (individual words).
     - `IntWritable`: The value for the output (the count of the word, initialized as `1`).

2. **Overriding the `map` Method**  
   ```java
   @Override
   protected void map(LongWritable key, Text value, Context context)
   ```
   - This method is executed once per input record.

3. **Processing the Line**  
   ```java
   String currentLine = value.toString();
   String[] words = currentLine.split(" ");
   ```
   - Converts the input `Text` value to a `String`.
   - Splits the line into words using a space `" "` as the delimiter.

4. **Emitting Key-Value Pairs**  
   ```java
   for (String word : words) {
       Text outputKey = new Text(word);
       context.write(outputKey, new IntWritable(1));
   }
   ```
   - Iterates through the words.
   - Converts each word into a `Text` object.
   - Writes the word (`outputKey`) and its initial count (`1`) to the context.

### How It Works:
- The mapper processes each line in an input file.
- It extracts words from the line and emits them as `(word, 1)`.
- These key-value pairs are passed to the reducer, which sums the occurrences of each word.

This `WordCountReducer.java` class is part of the Hadoop MapReduce Word Count program, designed to aggregate word occurrences counted by the `WordCountMapper`.

### **Explanation of the Code**
1. **Class Definition**  
   ```java
   public class WordCountReducer extends Reducer<Text, IntWritable, Text, IntWritable>
   ```
   - It extends the `Reducer` class with the following generic types:
     - `Text`: Represents the key (the word).
     - `IntWritable`: Represents the value (word count).
     - `Text`: Output key (same word).
     - `IntWritable`: Output value (final count of occurrences).

2. **Overriding the `reduce` Method**  
   ```java
   @Override
   protected void reduce(Text key, Iterable<IntWritable> values, Context context)
   ```
   - The `reduce` method is executed once per unique word (key) that was emitted by the mapper.

3. **Summing Up Word Occurrences**  
   ```java
   int sum = 0;
   for (IntWritable count : values) {
       sum += count.get();
   }
   ```
   - Iterates through the list of `IntWritable` values (each representing a `1` from the mapper).
   - Accumulates the total count for the word.

4. **Writing the Final Word Count**  
   ```java
   IntWritable outputValue = new IntWritable(sum);
   context.write(key, outputValue);
   ```
   - Creates a new `IntWritable` object for the final count.
   - Writes the `(word, total count)` pair to the context.

### **How It Works**
- The reducer receives intermediate `(word, 1)` pairs from the mapper.
- It aggregates all occurrences of each word.
- Outputs the final count as `(word, total occurrences)`, ready for storage or further processing.

WordCount represents YARN.

---

Running a MapReduce Job
To run a job, perform the following steps:
• Put the input files into HDFS
• If the output directory exists, delete it
• Use hadoop to execute the job
• View the output files

yarn jar wordcount.jar
my.WordCountJob input/file.txt result

yarn jar [jarfilename] [package_name].[class_name] [textfile] [foldername to store the output]

Execution
# Executable Jar vs Normal Jar

---

Shell Script:

Doc Comments:

# Author
# Date Created
# Modification Date
# Description
# Usage

--- 

vim and nano are command line editors
all installation is by default present in nano
nano is simpler than vim in terms of accessing and using commands

^ symbol in nano editor is known as [Ctrl] key.
M in nano editor is known as [Alt] key.

To save file in nano, use CTRL + O > ENTER > CTRL + X

---

nano test.sh

#!/bin/bash

#Author: Priyanka
#Date Created: 03-05-2025
#Modification Date: 03-05-2025
#Description: This is the first nano file
#Usage: doc/test.sh

$(hdfs dfs -test -e /user/talentum/)
#if [[ $? -eq 0 ]]; then
#echo "Path Exists..!!"
#else
#echo "Path Doesn't Exists..!!"
#fi

a=$(echo "Hello")
echo $a

![image](https://github.com/user-attachments/assets/96d9fbb2-6e49-453d-9d0e-b8d21c4d0d6c)

Output:

bash test.sh
Hello

![image](https://github.com/user-attachments/assets/9b45997b-c57d-4eb3-bbf0-8fa87de20bcb)

---

After if keyword, use square bracket.
if hdfs dfs -ls: This will return exit status

---

Whenever there is a code repetition, it is an opportunity to create a function

We can create libraries of functions and then we can use them.

---

Flow of execution of this command:

yarn jar invertedindex.jar <Main class> inverted/ inverted/output

First Main method will be triggered
Then ToolRunner will execute the run method
Configuration conf = super.getConf();

Path in = new Path(args[0]);
Path out = new Path(args[1]);

This is input (inverted) in args[0] and inverted/output in args[1]
from
yarn jar invertedindex.jar <Main class> inverted/ inverted/output

Yarn is responsible for launching instances of Mapper classes.

---

This is the code for this MapReduce implementation:

```java

package inverted;

import java.io.IOException;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

public class IndexInverterJob extends Configured implements Tool {

	public static class IndexInverterMapper extends
			Mapper<LongWritable, Text, Text, Text> {

		private Text outputKey = new Text();
		private Text outputValue = new Text();

		//TODO
		@Override
		protected void map(LongWritable key, Text value, Context context)
				throws IOException, InterruptedException {
			String [] words = value.toString().split(",");
			outputValue.set(words[0]);
			for(int i = 1; i < words.length; i++) {
				outputKey.set(words[i]);
				context.write(outputKey, outputValue);
			}
		}
	}

	//TODO
	public static class IndexInverterReducer extends
			Reducer<LongWritable,Text, Text, Text> {
		private Text outputValue = new Text();

		//TODO

		protected void reduce(Text key,  Iterable<Text> values, Context context)
				throws IOException, InterruptedException {
			StringBuilder builder = new StringBuilder();
			for(Text value: values) {
				builder.append(value.toString()).append(",");
			}
			builder.deleteCharAt(builder.length() - 1);
			outputValue.set(builder.toString());
			context.write(key, outputValue);
		}

	}


	public int run(String[] args) throws Exception {
		Configuration conf = super.getConf();
		Job job = Job.getInstance(conf, "IndexInverterJob");
		job.setJarByClass(IndexInverterJob.class);

		Path in = new Path(args[0]);
		Path out = new Path(args[1]);
		out.getFileSystem(conf).delete(out, true);
		FileInputFormat.setInputPaths(job, in);
		FileOutputFormat.setOutputPath(job,  out);

		//TODO
		job.setMapperClass(IndexInverterMapper.class);
		//TODO
		job.setReducerClass(IndexInverterReducer.class);

		job.setInputFormatClass(TextInputFormat.class);
		job.setOutputFormatClass(TextOutputFormat.class);

		//TODO
		job.setMapOutputKeyClass(Text.class);
		job.setMapOutputValueClass(Text.class);
		//TODO
		job.setOutputKeyClass(Text.class);
		job.setOutputValueClass(Text.class);

		return job.waitForCompletion(true)?0:1;
	}

	public static void main(String[] args) {
		int result;
		try {
			//TODO
			result = ToolRunner.run(new Configuration(),
					new IndexInverterJob(), args);
			System.exit(result);
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}

//Use following command to run the application
//$>	yarn jar invertedindex.jar <Main class> inverted/ inverted/output

```

This is the original hortonworks.txt file:

http://hortonworks.com/,hadoop,webinars,articles,download,enterprise,team,reliability
http://hortonworks.com/products/,hortonworks,services,core,feed,deployments,board,required
http://hortonworks.com/products/hortonworksdataplatform/,apache,password,directors,enterprise
http://hortonworks.com/get-started/,data,downloads,founders,hdp,deployments
http://hortonworks.com/download/,register,hadoop,hdp,download,presentations,videos
http://hortonworks.com/community/,connect,password,download,articles,knowledgebase,hadoop
http://hortonworks.com/kb,platform,feed,core,hadoop
http://hortonworks.com/about-us/,about,hortonworks,apache,hadoop,founders,directors
http://hortonworks.com/about-us/contact-us/,contact,support,hortonworks,hdp,enterprise
http://hortonworks.com/resources/,hadoop,services,training,videos
http://hortonworks.com/events/,hdp,downloads,platform,training,videos
http://hortonworks.com/webinars/,webinar,hadoop,videos,hdp
http://hortonworks.com/resources/,feed,blog,platform,hadoop,presentations,reliability
http://hortonworks.com/hadoop-training/,hadoop,instructor-led,certification,training,courses,learn,hdp

In Mapper Phase,
k1, v1 are paased and then k2, v2 are generated.

k1 will contain only the link and v1 will contain hadoop,webinars,articles,download,enterprise,team,reliability

After mapper phase, k2, v2 are generated.
k2 "hadoop"
v2 list: hortonworks.com/, hortonworks.com/products, 
hortonworks.com/products/hortonworksdataplatform/
hortonworks.com/get-started/
.
.
.
.
. and so on

---

Reducer Phase:

reduce(Text key,  Iterable<Text> values, Context context)

Text key represents Hadoop
Iterable<Text> values represents values (v2) -> Output values of Mapper Phase

---

This is the output of the whole program where the output file is stored in hdfs:

hdfs dfs -cat IndexInverterJob_output/part-r-00000
about	http://hortonworks.com/about-us/
apache	http://hortonworks.com/products/hortonworksdataplatform/
apache	http://hortonworks.com/about-us/
articles	http://hortonworks.com/community/
articles	http://hortonworks.com/
blog	http://hortonworks.com/resources/
board	http://hortonworks.com/products/
certification	http://hortonworks.com/hadoop-training/
connect	http://hortonworks.com/community/
contact	http://hortonworks.com/about-us/contact-us/
core	http://hortonworks.com/products/
core	http://hortonworks.com/kb
courses	http://hortonworks.com/hadoop-training/
data	http://hortonworks.com/get-started/
deployments	http://hortonworks.com/products/
deployments	http://hortonworks.com/get-started/
directors	http://hortonworks.com/about-us/
directors	http://hortonworks.com/products/hortonworksdataplatform/
download	http://hortonworks.com/download/
download	http://hortonworks.com/community/
download	http://hortonworks.com/
downloads	http://hortonworks.com/get-started/
downloads	http://hortonworks.com/events/
enterprise	http://hortonworks.com/products/hortonworksdataplatform/
enterprise	http://hortonworks.com/
enterprise	http://hortonworks.com/about-us/contact-us/
feed	http://hortonworks.com/products/
feed	http://hortonworks.com/resources/
feed	http://hortonworks.com/kb
founders	http://hortonworks.com/get-started/
founders	http://hortonworks.com/about-us/
hadoop	http://hortonworks.com/
hadoop	http://hortonworks.com/hadoop-training/
hadoop	http://hortonworks.com/resources/
hadoop	http://hortonworks.com/webinars/
hadoop	http://hortonworks.com/resources/
hadoop	http://hortonworks.com/about-us/
hadoop	http://hortonworks.com/kb
hadoop	http://hortonworks.com/community/
hadoop	http://hortonworks.com/download/
hdp	http://hortonworks.com/webinars/
hdp	http://hortonworks.com/download/
hdp	http://hortonworks.com/get-started/
hdp	http://hortonworks.com/events/
hdp	http://hortonworks.com/about-us/contact-us/
hdp	http://hortonworks.com/hadoop-training/
hortonworks	http://hortonworks.com/products/
hortonworks	http://hortonworks.com/about-us/contact-us/
hortonworks	http://hortonworks.com/about-us/
instructor-led	http://hortonworks.com/hadoop-training/
knowledgebase	http://hortonworks.com/community/
learn	http://hortonworks.com/hadoop-training/
password	http://hortonworks.com/community/
password	http://hortonworks.com/products/hortonworksdataplatform/
platform	http://hortonworks.com/resources/
platform	http://hortonworks.com/kb
platform	http://hortonworks.com/events/
presentations	http://hortonworks.com/resources/
presentations	http://hortonworks.com/download/
register	http://hortonworks.com/download/
reliability	http://hortonworks.com/
reliability	http://hortonworks.com/resources/
required	http://hortonworks.com/products/
services	http://hortonworks.com/products/
services	http://hortonworks.com/resources/
support	http://hortonworks.com/about-us/contact-us/
team	http://hortonworks.com/
training	http://hortonworks.com/events/
training	http://hortonworks.com/resources/
training	http://hortonworks.com/hadoop-training/
videos	http://hortonworks.com/webinars/
videos	http://hortonworks.com/resources/
videos	http://hortonworks.com/download/
videos	http://hortonworks.com/events/
webinar	http://hortonworks.com/webinars/
webinars	http://hortonworks.com/

Distributed Processing System
was introduced by Google

Google File System: introduced MapReduce

Head First Java

Sumitabha Das: Linux

---

![image](https://github.com/user-attachments/assets/94daa7b8-aec6-4b52-8639-1895f8ed9824)

This image is a diagram illustrating the process of how data is handled in a **MapReduce** framework. The diagram breaks down the key steps involved in **distributed processing**, showing how input data moves through **Mappers**, intermediate stages, and finally to the **Reducer**.

### Breakdown of the Diagram:
1. **Input Split**: Data is broken into smaller chunks before processing.
2. **InputFormat**: Generates `<k1, v1>` key-value pairs for processing.
3. **Mapper**: Processes the input pairs and transforms them into `<k2, v2>` pairs.
4. **Map Output Buffer**: Temporarily stores Mapper output before spilling to disk.
5. **Spill Files**: When the buffer reaches a threshold, sorted records are written to spill files.
6. **Merge Spill Files**: Multiple spill files are merged into a single sorted file.
7. **Reducer Input**: The merged spill files become input for the Reducer.
8. **Reducer**: Processes and aggregates values for each key to produce final results.

Additionally, **NodeManager** is mentioned in the diagram, highlighting its role in managing the nodes involved in the process.

### Why It’s Important:
This flow visually explains how **large-scale data processing** happens in Hadoop. It provides a structured view of **data movement, storage, and computation**, helping understand how Hadoop optimizes processing by dividing work across multiple nodes.

![image](https://github.com/user-attachments/assets/b0772637-dd21-40ce-bf9f-0adcc25fa694)

This image illustrates the process of data flow in a Hadoop MapReduce framework. It shows how the output from the Mapper phase is transferred to the Reducer phase. The image is divided into two main sections: the **Mapper output** and the **Reducer input**.

### **Key Steps in the Data Flow:**
1. **Reducer Fetches Data** → The Reducer retrieves data from the Mapper output.
2. **In-Memory Buffer** → The fetched data is first stored in an in-memory buffer for temporary processing.
3. **Spill Files Creation** → Once the buffer reaches a threshold, it writes sorted data into spill files.
4. **Merging Spill Files** → Multiple spill files are merged into a single sorted file.
5. **Reducer Processing** → The merged data becomes the input for the Reducer, which aggregates results.
6. **Final Output to HDFS** → The Reducer processes and stores the final results in the Hadoop Distributed File System (HDFS).

### **Key Components in the Image:**
- **NodeManager** → Manages execution and resource allocation.
- **Buffer & Spill Files** → Intermediate storage before merging.
- **Merged Input** → The structured and optimized data used by the Reducer.
- **HDFS Storage** → Where the final output resides.

This diagram is useful for understanding **how Hadoop optimizes large-scale data processing** by handling intermediate results efficiently before passing them to the Reducer.

## About YARN

YARN = Yet Another Resource Negotiator

YARN splits up the functionality of the JobTracker in Hadoop 1.x into
two separate processes:

• ResourceManager: for allocating resources and scheduling
applications

• ApplicationMaster: for executing applications and providing
failover

ClassLoader gets loaded. It loads the class. It loads into the memory. Which memory? RAM Memory.
JVM process gets launched.
There is a stack. There is a heap.
Process is the running instance of a program.
JVM Process.

How is the program running?

Main is running on the top of the stack.
Then the function which is being called inside the main function will get on top of the main in the stack.
After execution, those functions will be eliminated in the reverse order of their call.

per application process. Whenever program terminates, it de-process.

---

## Open-Source YARN Use Cases

• Tez: improves the execution of MapReduce jobs
• Slider: for deploying existing distributed applications onto YARN
• Storm: for real-time computing
• Spark: a MapReduce-like cluster computing framework designed
for low-latency iterative jobs and interactive use from an
interpreter
• Open MPI: a high-performance Message Passing Library that
implements MPI-2
• Apache Giraph: a graph processing platform

---

## The Components of YARN

The ResourceManager communicates with the NodeManagers,
ApplicationMasters, and Client applications.

![image](https://github.com/user-attachments/assets/b8fdf72a-9a89-4933-9fcf-2d5f29324cb5)

This image illustrates **the components of YARN** (Yet Another Resource Negotiator) and their interaction in a **distributed computing environment**.

### **Key Components:**
1. **ResourceManager** 🖥️
   - The central authority managing resources across the cluster.
   - Communicates with other components to allocate resources efficiently.

2. **NodeManager** ⚙️
   - Manages resources on individual nodes.
   - Reports available resources to the ResourceManager.
   - Executes tasks as directed by the ResourceManager.

3. **ApplicationMaster** 🔗
   - Manages the execution of a specific application.
   - Requests resources from the ResourceManager.
   - Oversees the application's lifecycle and progress.

4. **Client Application** 🏢
   - The external program submitting tasks to YARN.
   - Sends job requests to the ResourceManager.

### **Workflow Summary:**
1. A **Client Application** submits a job to the **ResourceManager**.
2. The **ResourceManager** assigns an **ApplicationMaster** for the job.
3. The **ApplicationMaster** requests resources from the **ResourceManager**.
4. Once resources are allocated, the job runs on different **NodeManagers**.
5. The **NodeManagers** execute tasks and report progress back.

This architecture enables **efficient resource allocation**, **scalability**, and **multi-tenancy** in big data applications like **Hadoop**.


---

## Lifecycle of a YARN Application

![image](https://github.com/user-attachments/assets/011f7bfb-f514-49d7-a7b1-60d3ce41875d)

This image illustrates the **lifecycle of a YARN (Yet Another Resource Negotiator) application**, detailing how a job is processed within a YARN cluster.

### **Lifecycle Steps:**
1. **Client Submits Application** 📨
   - A client sends a request to the **ResourceManager** to run an application.

2. **ApplicationMaster Allocation** 🛠️
   - The ResourceManager identifies a **NodeManager** with available resources.
   - The **NodeManager** creates a container to launch the **ApplicationMaster**.

3. **ApplicationMaster Requests Resources** 🔄
   - The **ApplicationMaster** contacts the **ResourceManager** and requests necessary resources.
   - The **ResourceManager** provides a list of allocated containers.

4. **Task Execution in Containers** 🚀
   - Containers execute tasks within the **NodeManager**, processing data or computations as required.
   - The **ApplicationMaster** monitors the execution progress.
   - We can say containers as the JVM when working with Java.

5. **Completion & Resource Cleanup** ✅
   - Once tasks are completed, results are stored, and resources are released back to the YARN cluster.

### **Why This Matters?**
- YARN enables **efficient cluster resource management** for distributed applications.
- It allows multiple applications to run concurrently while optimizing resource allocation.
- Helps frameworks like **Hadoop** handle **big data processing** across multiple nodes.


This flow is all known as DISTRIBUTED PROGRAMMING.

---

## A Cluster View Example

![image](https://github.com/user-attachments/assets/b57a8e01-85e7-48ba-9c53-366fc5e49ba4)

On running localhost:8088 on Linux Browser, we see:

![image](https://github.com/user-attachments/assets/d5e2a862-838b-403d-a18c-cef532ebb519)

Here, we can see multiple application Ids.

This image titled **"A Cluster View Example"** illustrates the structure and operation of a YARN-based **computing cluster**. The diagram highlights the **ResourceManager**, **NodeManagers**, and their interaction with **Application Masters (AM)** and **Containers**.

### **Key Components in the Cluster:**
1. **ResourceManager** 🖥️
   - Manages the entire cluster's resources.
   - Includes a **Scheduler** that decides resource allocations.
   - Contains an **ApplicationMaster Scheduler (AsM)** to handle application requests.

2. **NodeManager** ⚙️
   - Runs on each node in the cluster.
   - Monitors resources and manages Containers.
   - Communicates with the ResourceManager.

3. **Application Masters (AM)** 🔗
   - Each application has its own Application Master.
   - The AM requests Containers from the ResourceManager.
   - Manages the execution of tasks across the cluster.

4. **Containers** 📦
   - Containers execute application tasks.
   - They are allocated dynamically by the ResourceManager.
   - Some nodes run both **Containers and AMs**, while others run only Containers.

### **Cluster Structure Insights:**
- **Nodes with Containers:** These execute computational workloads.
- **Nodes with Application Masters:** These coordinate the tasks.
- **Resource Allocation:** Containers are spread across various nodes for parallel execution.

### **Why This Architecture is Useful?**
- **Scalability:** Can dynamically adjust resources across a distributed system.
- **Efficiency:** Separates resource management from computation, optimizing performance.
- **Fault Tolerance:** Tasks can be redistributed if nodes fail.



















