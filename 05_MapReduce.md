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



















