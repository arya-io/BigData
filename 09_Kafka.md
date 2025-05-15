# 🚀 How Companies Start  

### Understanding Data Exchange in Business  
Before diving into **Kafka**, let's understand how companies begin handling data.

🔹 At the start, things are **simple**:  
   - There's **one** source system (where data is generated).  
   - There's **one** target system (where data is needed).  
   - These two systems **exchange data** between each other seamlessly.

![image](https://github.com/user-attachments/assets/aea045a7-28b2-45ce-a698-cad3b5b54013)

---

# ⚡ Scaling Up: More Systems, More Complexity  

🔹 As a company **grows**, things get complicated:  
   - **Multiple** source systems emerge, generating diverse data.  
   - **Multiple** target systems appear, each requiring different data.  
   - **Tight coupling** occurs, meaning systems become heavily dependent on each other.  
   - We **can't easily separate them**, making modifications a headache!  

📌 The more systems interact, the harder it becomes to **manage data flow**.

![image](https://github.com/user-attachments/assets/83960fc7-035f-4d38-9ade-becb21130480)

---

# ❌ Challenges in Traditional Architectures  

Let's say we have **4 source systems** and **6 target systems**.  
🔹 To **connect** them all, we'd need **24 integrations** 😵!  

Each integration comes with **major challenges**:  
✅ **Protocol Issues** – How should data move? (TCP, HTTP, REST, FTP, JDBC...)  
✅ **Data Format Problems** – How should we structure data? (Binary, CSV, JSON, Avro...)  
✅ **Data Schema Evolution** – How will data **change** over time?  
✅ **High System Load** – Every new connection **adds stress** to the system.  

🎯 **Clearly, this isn’t scalable!** Companies **struggle** to manage data efficiently.  
So... how do we **solve** this problem? 🤔  

---

# 🌟 Solution: Apache Kafka  

🎯 This is where **Apache Kafka** comes in! 🚀  

🔹 Kafka **decouples** data streams, making systems **independent**.  
🔹 Now, instead of direct exchanges between systems:  
   - **Source systems** send data to **Kafka**.  
   - **Target systems** **fetch data** from **Kafka**.  

💡 **No more tight coupling!** Kafka acts as a **middle layer**, simplifying data flow.

![image](https://github.com/user-attachments/assets/4adf3bc9-5877-4b2b-a167-6c5a1b64e81f)

---

# 🔄 Kafka Enables Flexible Data Flow  

Kafka allows **any type of data stream** to flow through it:  
✅ Log files  
✅ Transactions  
✅ Sensor data  
✅ Messages from applications  

🔹 Once data is inside **Kafka**, it can be sent to **any system** efficiently!  
📌 Think of it as a **super-fast messenger** that **delivers data smoothly**. 🚀  

![image](https://github.com/user-attachments/assets/589a18b7-84c4-4dea-ab97-29c210a9ebb0)

---

# 🌍 Why Apache Kafka?  

### Origins & Growth 📌  
🔹 **Kafka** was originally developed by **LinkedIn** and is now an **open-source** project.  
🔹 It's mainly maintained by **Confluent**, but it falls under the **Apache Foundation** stewardship.  

### Why is Kafka Powerful?  
✅ **Distributed Architecture** – Handles data across multiple machines.  
✅ **Resilient & Fault-Tolerant** – Can **recover** from failures (similar to RDD in Spark and fault tolerance in Hadoop).  
✅ **Scales Horizontally** – Easily adds more machines to process high data volumes.  
✅ **Massive Clusters** – Some Kafka setups have **100+ brokers** handling data.  
✅ **High Throughput** – Proven by LinkedIn & others to process **millions** of messages per second.  
✅ **Low Latency (Real-Time Processing)** – In optimal conditions, Kafka transfers data between systems in **less than 10ms**!  

📌 **Real-time** = Super low latency = Instant data flow ⚡  

---

# 🏢 Who Uses Apache Kafka?  

Kafka plays a key role in real-time systems at top companies:  
🔹 **Airbnb** – Real-time analytics for customer interactions  
🔹 **LinkedIn** – Spam detection & recommendations  
🔹 **Uber** – Real-time demand forecasting & surge pricing  
🔹 **Walmart** – Logistics tracking  
🔹 **Netflix** – Instant content recommendations  

![image](https://github.com/user-attachments/assets/511343c7-2427-4916-9614-ca65088e7e12)

---

# 🔍 Apache Kafka: Core Use Cases  

Kafka solves several critical data challenges:  

✅ **Messaging System** – Acts as a high-speed event bus for passing data.  
✅ **Activity Tracking** – Gathers metrics from various sources, including IoT devices.  
✅ **Application Logging** – Collects logs for debugging, monitoring, and analysis.  
✅ **Stream Processing** – Enables real-time data manipulation via Kafka Streams API or **Spark**.  
✅ **Decoupling Dependencies** – Reduces complexity between interacting systems.  
✅ **Big Data Integration** – Works seamlessly with **Spark, Flink, Storm, Hadoop**, and more!  

---

# 🌟 Kafka in Action: Real-World Examples  

Kafka is a **backbone technology** for major businesses:  

🔹 **Netflix** – Uses Kafka to **recommend** shows **instantly** after a user finishes watching.  
🔹 **Uber** – Relies on Kafka to collect **user, taxi, and trip data** and compute **surge pricing** dynamically.  
🔹 **LinkedIn** – Uses Kafka for **spam prevention**, **user behavior tracking**, and **connection recommendations** – all in **real-time**!  

---

# 🔥 Why Kafka is Game-Changing  

Companies use Kafka for **three key benefits**:  

✅ **Real-Time Recommendations** – Like Netflix suggesting your next show!  
✅ **Real-Time Decisions** – Uber adjusting prices based on demand.  
✅ **Real-Time Insights** – Businesses analyzing customer behavior instantly.  

📌 **But remember**, Kafka is just a **transport mechanism**!  
📌 Applications still **need logic** to process and use data effectively.  
📌 Kafka ensures **data moves FAST at scale!** 🚀  

---

# 🏗️ Kafka Fundamentals  

### 🎯 Topics, Partitions & Offsets  
Kafka organizes data into **topics**, which are like database **tables**:  
✅ **Topics** – A categorized stream of data (e.g., GPS locations, logs).  
✅ **Partitions** – Topics are **split** into partitions for **parallelism**.  
✅ **Ordered Messages** – Each partition maintains an **ordered sequence**.  
✅ **Offsets** – Each message gets a **unique ID** (**incremental counter**) for tracking.  

📌 Kafka stores **an infinite** number of messages over time—data **never stops** flowing! 🌊  

![image](https://github.com/user-attachments/assets/097b49a7-273c-4cfc-b1b3-49a4da50c51a)

---

# 🚚 Topic Example: `trucks_gps`  

### 🚛 Real-Time Truck Tracking with Kafka  
🔹 Imagine a **fleet of trucks**, each reporting **GPS** location data.  
🔹 Kafka can handle a **trucks_gps** topic, storing positions for all trucks.  
🔹 Each truck **sends a message** every **20 seconds** containing:  
   - **Truck ID**  
   - **Latitude & Longitude**  

📌 The topic can have **10 partitions** to distribute load efficiently.  

🔹 Two applications use this data:  
✅ **Location Dashboard** – Displays truck positions visually.  
✅ **Notification Service** – Alerts users when trucks enter/exist regions.  

![image](https://github.com/user-attachments/assets/bda5c912-09bd-4db0-b7ae-38ccceac9d3a)

---

# 🏗️ Kafka Fundamentals: Topics, Partitions & Offsets  

### 🔍 Understanding Offsets in Kafka  

Kafka breaks data into **topics**, which are further divided into **partitions**.  
Each partition ensures **message ordering** and assigns an **offset** (a unique ID).  

✅ **Offsets only apply within a single partition** – meaning:  
   - Offset **3 in Partition 0** ≠ Offset **3 in Partition 1** – **They hold different data!**  
✅ **Ordering is only guaranteed within a partition**, not across multiple partitions.  
✅ **Data retention is temporary** – usually **one week** by default.  
✅ **Immutability** – Once data is **written**, it **cannot be changed**.  
✅ **Random partition assignment** – Unless a **key** is provided, Kafka assigns data randomly.  

📌 Kafka ensures fast and **reliable** data processing while keeping old data available for a limited time.  

![image](https://github.com/user-attachments/assets/931a0100-732f-4bee-b875-da013afd3f7f)

---

# 💡 Brokers: The Backbone of Kafka  

### 🔎 What Are Brokers?  
A **Kafka cluster** is made up of **brokers** – powerful servers that store and manage data.  

✅ **Brokers hold topics & partitions**, acting as storage nodes.  
✅ **Each broker** has a unique **ID** (integer).  
✅ **Each broker contains different partitions from multiple topics**.  
✅ Once connected to **any broker** (called a **bootstrap broker**), you are connected to the **entire cluster**.  
✅ A beginner-friendly setup starts with **3 brokers**, but massive clusters **can have 100+ brokers**!  

📌 **Think of brokers as the "warehouse managers" of Kafka** – they ensure data storage and accessibility at scale!  

![image](https://github.com/user-attachments/assets/81b502f9-4e98-4618-8a5b-cc4ce6112abf)

---

# 🔄 Brokers & Topics: Data Distribution  

Kafka distributes **topics and partitions** across multiple brokers for **scalability**.  

Example setup:  
✅ **Topic-A** with **three partitions**, spread across **three brokers**.  
✅ **Topic-B** with **two partitions**, but **Broker 103 doesn’t store any Topic-B data**.  

📌 Data gets **spread efficiently** among brokers, preventing overload on a single machine.  

![image](https://github.com/user-attachments/assets/4abfb86a-192f-4a09-8764-084f8665b4b9)

---

# 🛠️ Fault Tolerance: Topic Replication Factor  

Kafka ensures **data resilience** through replication.  

✅ **Replication Factor** > 1 ensures **fault tolerance**.  
✅ Standard replication is **2 or 3** copies per partition.  
✅ If **one broker fails**, other brokers **still serve the data**.  

### 🔥 Real-World Example  
🎯 **Cluster with 3 Brokers**  
🎯 **Topic-A with 2 partitions & replication factor = 2**  

🚨 **Broker 102 fails**…  
✅ **Broker 101 & 103 still have the data, ensuring zero data loss!**  

📌 **Replication is critical for Kafka clusters—it prevents failures from disrupting data flow!**  

![image](https://github.com/user-attachments/assets/c368d58e-8abe-45e1-beae-4c04ec9efea9)  

🔥 Even if **one server goes down**, **Kafka ensures business continuity**.  

![image](https://github.com/user-attachments/assets/13408999-7909-4fc0-a074-41516c287e21)

---

# ⚡ Concept of Leader for a Partition  

Kafka **organizes data into partitions**, but **who manages** them?  

### 🔹 Partition Leadership  
✅ **Only ONE broker** acts as the **leader** for each partition at a time.  
✅ **The leader broker** is responsible for **receiving & serving data** for that partition.  
✅ **Other brokers act as followers** and **synchronize the data** from the leader.  
✅ Each partition has **one leader** and multiple **ISRs (In-Sync Replicas)**.  

📌 If the leader broker **fails**, Kafka **elects** a new leader automatically to **ensure data availability**.  

![image](https://github.com/user-attachments/assets/3bf28d1d-3290-451a-9bfd-2ec101fbb3f0)

---

# 📝 Producers: Writing Data to Kafka  

### 🔎 What Are Producers?  
Producers are applications that **write data** to Kafka topics.  
✅ Producers **automatically decide** which **broker** and **partition** to send data to.  
✅ If a **broker fails**, producers **auto-recover** to prevent disruption.  

📌 Think of **producers** as **data suppliers**—sending messages efficiently into Kafka!  

![image](https://github.com/user-attachments/assets/7a072ff1-3d5d-49c5-9d6b-d3aed228c9b3)

---

# 🔄 Producer Acknowledgements (acks)  

Kafka provides **three levels** of **data write acknowledgements**:  

✅ **acks=0** – Producer **does not wait** for confirmation (fastest, but risk of **data loss**).  
✅ **acks=1** – Producer waits for **leader acknowledgement** (**low risk** of data loss).  
✅ **acks=all** – Leader **plus all in-sync replicas** acknowledge the write (**no data loss**).  

📌 **Stronger acknowledgements = Higher data safety** 🔥  

![image](https://github.com/user-attachments/assets/acfecfbb-0b18-4465-9be1-c8f8417a8caa)

---

# 🔑 Producers & Message Keys  

### Why Use Keys?  
✅ **Producers can attach a key** (e.g., **truck ID, user ID**) to each message.  
✅ If **key=null**, messages are **sent randomly** in a **round-robin** fashion across partitions.  
✅ If a **key is provided**, all messages with the same key **go to the same partition**.  
✅ This is **essential for maintaining order** in case-specific fields need sequential tracking.  

📌 Example:  
🚚 **Tracking Truck GPS Data** – All messages from a **specific truck ID** must go into the **same partition** for accurate ordering.  

![image](https://github.com/user-attachments/assets/61b03f6c-e897-489b-a015-a98be1df78c2)

---

# 📥 Consumers: Reading Data from Kafka  

### 🔹 What Are Consumers?  
Consumers are applications that **read and process data** from Kafka topics.  
✅ **Each consumer reads from a topic** identified by its **name**.  
✅ Consumers **automatically know** which broker to fetch data from.  
✅ If a **broker fails**, consumers **adjust** to read data from another available broker.  
✅ **Data is read in order within each partition** – ensuring **structured sequencing**.  

📌 **Consumers act as "data receivers," ensuring messages are properly retrieved and processed!**  

![image](https://github.com/user-attachments/assets/8964535b-df13-40c1-a275-ed2581b30841)

---

# 🔄 Consumer Groups: Parallel Data Processing  

### 🔍 What Are Consumer Groups?  
Consumers **read data efficiently** using **consumer groups**.  

✅ A **consumer group** allows multiple consumers to **share the workload**.  
✅ Each **consumer in the group** reads from **exclusive partitions**—ensuring **parallel processing**.  
✅ If there are **more consumers than partitions**, **some consumers remain inactive**.  

📌 **Consumers work together to distribute the data load!**  

![image](https://github.com/user-attachments/assets/add1a59c-3ae4-41db-832d-7ab501d423b1)

---

# ❓ Too Many Consumers?  

### 🔎 What Happens If We Have More Consumers Than Partitions?  
✅ Kafka **assigns one partition per active consumer**.  
✅ If the **number of consumers exceeds partitions**, extra consumers **become inactive**.  
✅ They stay **connected** but **do not receive data** until partitions **increase** or **existing consumers drop off**.  

📌 **Always ensure the number of consumers aligns with partitions for efficient scaling!**  

![image](https://github.com/user-attachments/assets/1b6006cc-14ec-4eae-9b62-e9a76e7d7615)

---

# 📌 Consumer Offsets: Tracking Read Data  

### 🔎 What Are Consumer Offsets?  
✅ Kafka **stores offsets** tracking the last read message for **each consumer group**.  
✅ These offsets live in a **special Kafka topic** called `__consumer_offsets`.  
✅ When a **consumer processes data**, it commits **the offset** for future retrieval.  
✅ If a **consumer crashes**, it can **resume reading** from the last committed offset.  

📌 **Offsets help ensure data continuity and prevent re-processing errors!**  

![image](https://github.com/user-attachments/assets/1248f177-0a2f-43a9-9c29-f95b49b7dbfb)

---

# 🎯 Consumer Delivery Semantics: Ensuring Reliability  

Consumers decide **when to commit offsets**, impacting **data reliability**.  

### 🔄 Three Delivery Semantics  

✅ **At Most Once** – Offsets are committed **as soon as the message is received**.  
   - 🚨 If processing **fails**, the message is **lost forever**!  

✅ **At Least Once** (Most Common) – Offsets are committed **after processing**.  
   - ⚠ If processing **fails**, the message **is re-read**, causing **possible duplicates**.  
   - 🛠 **Solution**: Make processing **idempotent** (re-processing should not impact results).  

✅ **Exactly Once** – Ensures **no duplicate reads** (Best reliability).  
   - 🔹 Achieved **within Kafka** using **Kafka Streams API**.  
   - 🔹 For **external system workflows**, use **an idempotent consumer**.  

📌 **Choosing the right delivery semantics is critical to avoid data loss and duplication!**  

---

# 🔎 Kafka Broker Discovery  

### 🔹 What Are Bootstrap Servers?  
✅ Every Kafka **broker** is known as a **bootstrap server**.  
✅ This means connecting to **any single broker** gives access to the **entire Kafka cluster**.  
✅ Each broker **stores metadata**, knowing about **all other brokers, topics, and partitions**.  

📌 **Connect to one broker, and you’re connected to them all!** 🚀  

![image](https://github.com/user-attachments/assets/b6056ef0-d49e-496b-b323-8f896ba1d984)

---

# 🛠️ Zookeeper: The Backbone of Kafka  

### 🔎 Why Does Kafka Need Zookeeper?  
Zookeeper acts as Kafka’s **management system**, ensuring coordination across brokers.  

✅ **Tracks brokers** – Maintains a list of all active Kafka brokers.  
✅ **Handles leader election** – Decides which broker will lead each partition.  
✅ **Sends notifications** – Alerts Kafka when **brokers fail**, **new brokers join**, or **topics are modified**.  
✅ **Operates in odd-numbered clusters** – Usually **3, 5, or 7 servers** for **high availability**.  
✅ **Leader & Followers** – One **Zookeeper node** acts as the **leader** (handles writes), others as **followers** (handle reads).  
✅ **No Offset Storage** – Zookeeper **stopped storing consumer offsets** in Kafka **versions > 0.10**.  

📌 Without Zookeeper, Kafka **cannot function properly**!  

![image](https://github.com/user-attachments/assets/b2fe444f-33db-4767-a76f-8863c1ec89a4)

---

# 🔄 Kafka Guarantees  

Kafka ensures **strong data reliability and consistency** with key guarantees:  

✅ **Ordered Message Processing** –  
   - Messages are **appended to a topic-partition** in **the order they’re sent**.  
   - Consumers read messages **in the same order they were stored**.  

✅ **High Fault Tolerance** –  
   - With a **replication factor of N**, producers/consumers can tolerate **up to (N-1) broker failures**.  
   - A **replication factor of 3** is ideal:  
     - Allows **one broker to be taken down** for maintenance.  
     - Allows **another broker to fail unexpectedly** without losing data.  

✅ **Consistent Message Routing** –  
   - As long as the **number of partitions remains constant**, messages with the same **key** always go to the **same partition**.  

📌 Kafka ensures **resilient and scalable** message handling while maintaining strict data ordering!  

---

# 🎯 Theory Roundup  

Kafka guarantees **distributed, scalable, and fault-tolerant** messaging—enabling businesses to handle **real-time data** efficiently.  

![image](https://github.com/user-attachments/assets/4a8fb287-23f8-49ea-a7d9-663d85939b55)

---

# Implementation of Kafka

Launch Zookeeper
bash run-kafka_zookeeper_server.sh -s start

Launch server
bash run-kafka_server.sh -s start

You should see Kafka running through jps and QuorumPeerMain
talentum@talentum-virtual-machine:~$ jps
1796 RunJar
2472 SparkSubmit
873 SecondaryNameNode
9099 Kafka
1196 NodeManager
463 NameNode
9456 Jps
3986 SparkSubmit
1043 ResourceManager
2324 SparkSubmit
2708 Main
8791 QuorumPeerMain
635 DataNode

kafka-topics.sh
Shows entire documentation

Create a topic
kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create

If error occurs in Kafka, it does not show error, but the documentation.

kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3
Still shows documentation
Partition cannot exists without replication factor

kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 2
partition is 3 but replication is 2 so 6 partitions will be created
After running this command, got a warning: Error while executing topic command : Replication factor: 2 larger than available brokers: 1.

kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1
Created topic first_topic.

kafka-topics.sh --zookeeper 127.0.0.1:2181 --list
List the topics
2181 --list
first_topic


kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --describe
Describe the topics
2181 --topic first_topic --describe
Topic:first_topic	PartitionCount:3	ReplicationFactor:1	Configs:
	Topic: first_topic	Partition: 0	Leader: 0	Replicas: 0Isr: 0
	Topic: first_topic	Partition: 1	Leader: 0	Replicas: 0Isr: 0
	Topic: first_topic	Partition: 2	Leader: 0	Replicas: 0Isr: 0

kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic second_topic --delete
Delete the topic

---

# Console Producer

kafka-console-producer.sh

kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic
>Hello Priyanka
>It's a good day..!!
>How are you?
>I am good here.
>^C

These messages went into topic.

This is an example of asynchronous communication

kafka-console-producer.sh --broker-t 127.0.0.1:9092 --topic first_topic --producer-property acks=all
>Hello
>Today is Thursday
>We are going on a trip next Wednesday
>^C
This has set the acknowledgment mode

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic
Nothing happens

---

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic
Read messages here

kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic first_topic
Write messages here

Communication has been established

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning
How are you?
Today is Thursday
Good day
Hello Priyanka
I am good here.
We are going on a trip next Wednesday
hello
It's a good day..!!
Hello
hi Priyanka
jj

Shows messages right from the beginning

Messages are displayed in random order. Why?

---

How to launch consumer group? -- IMPLEMENTATION

We have a topic - first topic
In that we have three partitions
and it forms a cluster

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application
This is our consumer 1

kafka-console-producer.sh --broker-t 127.0.0.1:9092 --topic first_topic
Now producer is running
M1 is message is passed
Consumer gets this message
Now M2

Messages go in round robin fashion
Now M3 message is produced

All these three messages went to three partitions

To decrease the load on the group, we will launch another consumer in the same group

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application
This is our consumer 2 and it has been launched through above command

Now more messages are produced and they are consumed by another consumer

Now we are launching another consumer. This will be our consumer 3 belonging to the same consumer group

kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application

Messages are produced till M8
M8 went to third consumer
M9 went to second consumer
M10 went to first consumer

Now we launched consumer 4
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application

M11 went to fourth consumer
M12 went to third consumer
M13 went to first consumer
M13 went to fourth consumer
M15 to third
M16 to first

We crashed the fourth consumer. 
M17 to third
M18 to second
M19 to first

Every consumer is commiting the offset
Producer is a software program whose responsibility is the create the messages
and Consumers reads the messages

Whenever a consumer is crashed, another consumer takes its place.

---
