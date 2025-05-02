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