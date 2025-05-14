## How Companies Starts
 So before we learn about Kafka, let's learn how companies starts
 At first it's super simple. You get a source system, and you have a target 
system
 And then you need to exchange data

![image](https://github.com/user-attachments/assets/aea045a7-28b2-45ce-a698-cad3b5b54013)


## After a while...
 What happens is...
 You have many source systems, and many target systems
 They all have to exchange data with one another, and things become really 
complicated
There is a tight coupling, we cannot separate

![image](https://github.com/user-attachments/assets/83960fc7-035f-4d38-9ade-becb21130480)


## Problems Organizations are facing with 
previous architecture
 If we have four source systems and six target systems; You need 
to have 24 integrations to write
 Each integration as you may or may not know, comes with a lot 
of difficulties around
 Protocol - how the data is transported (TCP, HTTP, REST, FTP, JDBC....)
 The data format - how the data is parsed (binary, CSV, JSON, Avro, Thrift 
and others....)
 The data schema and evolution - so how the data is shaped and how it may 
change in the future
 Additionally, each time you integrate a source system with the 
target system, there will be an increased load from the 
connections

How do we solve this?

---

## Why Apache Kafka: Decoupling of data 
streams and systems
 Well this is where Apache Kafka comes in
 Apache Kafka, allows you to decouple your data streams and 
your systems
 So now your source systems will have their data end up in Apache Kafka
 While your target systems will source their data straight from Apache 
Kafka

![image](https://github.com/user-attachments/assets/4adf3bc9-5877-4b2b-a167-6c5a1b64e81f)

---

## Why Apache Kafka: Decoupling of data 
streams and systems
 So for example, what do we have in Kafka?
 Well you can have any data stream you can think about
 Additionally, once the data is in Kafka, you may want to put it into any 
system you like
Stream which is continuously coming, here it means data

![image](https://github.com/user-attachments/assets/589a18b7-84c4-4dea-ab97-29c210a9ebb0)

---

## Why Apache Kafka
 It was created by LinkedIn, and it's now an open source project, 
mainly maintained by a private company called Confluent. But 
it's under the Apache stewardship
 It's distributed, resilient (withstanding the failures) architecture, and fault tolerant (RDD is resilient and Hadoop is fault tolerant)
 It scales horizontally
 There are Kafka clusters with over 100 brokers
 It is proven by LinkedIn and many other companies, that it can scale to 
millions of messages exchanged per second
 High performance (the latency to exchange data from one system to 
another is usually less than 10 millisecond) if you have good machines. And 
this is what we call real time

Real time means that the 
latency is really really low

---

Why Apache Kafka?
airbnb
Linkedin
Uber
Walmart
Netflix


![image](https://github.com/user-attachments/assets/511343c7-2427-4916-9614-ca65088e7e12)

---

## Apache Kafka: Use cases
 Messaging system
 Activity tracking by gather metrics from many different locations 
or your IoT devices
 Gather logs from your applications
 Stream processing (Using Kafka streams API, or with Spark as an 
example)
 De-coupling of system dependencies
 Integration with Spark, Flink, Storm, Hadoop, and other big data 
technologies

---

## Kafka examples...
 So considering a wide array of use cases, many companies are 
using Apache Kafka as their backbone in their systems
 Netflix is using Kafka to apply recommendations in real time while you're 
watching TV shows (And this is why, basically, when you leave a TV show, 
you'll get a new recommendation right away)
 Uber uses Kafka to gather user, taxi, and trip data in real time to compute 
and forecast demand, and computes the surge pricing in real time
 LinkedIn uses Kafka to prevent spam, and their platform, collect user 
interactions and make better connection recommendations all of that in 
real time

---

## Kafka examples...
 Basically as you can see, all these companies are using Kafka so 
that they can make
 real time recommendation
 real time decisions
 give real time insights to their users
 Remember that, Kafka is only used as a transportation 
mechanism
 People need, will still write their applications or web applications to make 
things work, but Kafka is really good at making your data move really fast 
at scale

---

# Kafka Fundamentals

## Topics, partitions and offsets
 Topics – A particular stream of data
 It's basically similar to a table in a database1
 you can have as many topics as you want
 A topic is going to be identified by its name
 Topics are split into partitions2
 Each partition is ordered
 Each message within a partition gets an incremental id called as offset
It is infinite, Unbounded

![image](https://github.com/user-attachments/assets/097b49a7-273c-4cfc-b1b3-49a4da50c51a)

---

## Topic example – trucks_gps

![image](https://github.com/user-attachments/assets/bda5c912-09bd-4db0-b7ae-38ccceac9d3a)

 Say you have a fleet of trucks, each truck reports its gps position 
to kafka
 You can have a topic trucks_gps that contains the position of all 
trucks
 Each truck will send a message to kafka every 20 seconds, each 
message will contain the truck id and the truck position (latitude 
and longitude
 We choose to create that topic with 10 partitions(arbitrary 
number)

Two appliations have been made:
Location Dashboard
Notification service.

---

## Topics, partitions and offsets

![image](https://github.com/user-attachments/assets/931a0100-732f-4bee-b875-da013afd3f7f)

 Offsets only have a meaning for a specific partition
 E.g. offset 3 in partition 0 doesn’t represent the same data as offset 3 in 
partition 1
 Order is guaranteed only within a partition (not across 
partitions)
 Data is kept only for a limited period (default is one week)
 Once the data is written to a partition, it cannot be changed 
(immutability)
 Data is assigned randomly to a partition unless a key is provided 
(more on this later)

---

$$ Brokers
 Okay, so we've talked about topics, but what holds the topics? 
What holds the partitions?
 The answer is a broker
 A Kafka cluster is composed of multiple brokers(servers)
 Each broker is identified with its id (Integer)
 Each broker contains certain topic partitions
 After connecting to any broker (called a bootstrap broker), you 
will be connected to the entire cluster
 A good number to get started is 3 brokers, but some big clusters 
have 100 brokers

![image](https://github.com/user-attachments/assets/81b502f9-4e98-4618-8a5b-cc4ce6112abf)

---

## Brokers and Topics
 We have 3 brokers
 Example of Topic-A with three partitions
 Example of Topic-B with two partitions

![image](https://github.com/user-attachments/assets/4abfb86a-192f-4a09-8764-084f8665b4b9)


 Note – Data is distributed and Broker 103 does not have any 
Topic-B data

---

Topic replication factor
 Kafka is a distributed system1
 So, when there's a distributed system in the big data world we 
need to have replication to achieve fault tolerance2

 Here is our cluster with three brokers
 Topics should have a replication factor > 1 (ususally between 2 
and 3)1
 This way if a broker is down, another broker can serve the data
 Example – Topic-A with 2 partitions and replication factor of 2

![image](https://github.com/user-attachments/assets/c368d58e-8abe-45e1-beae-4c04ec9efea9)

 Example: We lost broker 102
 Result: Broker 101 and 103 can still serve the data

![image](https://github.com/user-attachments/assets/13408999-7909-4fc0-a074-41516c287e21)

---

## Concept of Leader for a Partition 
 At any time only ONE broker can be a leader for a given partition
 Only that leader can receive and serve data for that partition
 The other brokers will synchronize the data
 Therefore each partition has one leader and multiple ISRs(Insync replica)

![image](https://github.com/user-attachments/assets/3bf28d1d-3290-451a-9bfd-2ec101fbb3f0)

---

## Producers
 Producers write data to topics(which is made up of partitions)
 Producers automatically know to which broker and partition to 
write to
 In case of broker failure, Producers will automatically recover

![image](https://github.com/user-attachments/assets/7a072ff1-3d5d-49c5-9d6b-d3aed228c9b3)

 Producers can choose to receive acknowledgement of data 
writes:
 acks=0: Producer won’t wait for acknowledgement (possible data loss)
 acks=1: Producer will wait for leader acknowledgement (limited data loss)
 acks=all: Leader + ISR acknowledgement (no data loss)

![image](https://github.com/user-attachments/assets/acfecfbb-0b18-4465-9be1-c8f8417a8caa)

---

## Producers: Message keys

 Producers can choose to send a key with message(string, 
number, etc…)
 If key=null data sent round robin
 If a key is sent, then all messages for that key will always go to 
the same partition
 A key is basically sent if you need message ordering for a specific 
field (eg – truck_id)

![image](https://github.com/user-attachments/assets/61b03f6c-e897-489b-a015-a98be1df78c2)

---

## Consumers
Consume means read and then process
 Consumers read data from a topic (identified by name)
 Consumers know which broker to read from
 In case of broker failures, consumers know how to recover
 Data is read in order within each partition

![image](https://github.com/user-attachments/assets/8964535b-df13-40c1-a275-ed2581b30841)

---

## Consumer groups
Reads the data parallely
 Now, how do these consumers read data from all the partitions?
 Consumers read data in consumer groups
 Each consumer within a group reads from exclusive partitions
 If you have more consumers than partitions, some consumers will 
be inactive

![image](https://github.com/user-attachments/assets/add1a59c-3ae4-41db-832d-7ab501d423b1)

---

## Consumer groups, what if too many 
consumers?
 If you have more consumers than partitions then some 
consumers will be inactive

![image](https://github.com/user-attachments/assets/1b6006cc-14ec-4eae-9b62-e9a76e7d7615)

---

## Consumer Offsets
 Kafka stores the offsets at which a consumer group has been 
reading
 These offsets committed live in a Kafka topic named 
__consumer_offsets
 When a consumer in a gropup has processed data received from 
Kafka, it should be committing the offsets
 If a consumer dies, it will be able to read back from where it left 
off thanks to the committed consumers offsets!

![image](https://github.com/user-attachments/assets/1248f177-0a2f-43a9-9c29-f95b49b7dbfb)

---

## Delivery semantics for consumers
 Consumers choose when to commit offsets
 There are 3 delivery semantics:
 At most once:
 Offsets are committed as soon as the message is received
 If the processing goes wrong, the message will be lost (It won’t be read again)
 At least once (usually preferred):
 Offsets are committed after the message is processed
 If the processing goes wrong, the message will be read again
 This can result in duplicate processing of messages. Make sure your processing 
is idempotent (i.e processing again the messages won’t impact your systems)
 Exactly once:
 Can be achieved for Kafks => Kafka workflows using Kafka Streams API
 For Kafka => External system work flows, use an idempotent consumer

---

## Kafka broker discovery
 Every Kafka broker is also called a “bootstrap server”
 That means that you only need to connect to one broker, and 
you will be connected to the entire cluster
 Each broker knows about all brokers, topics, and partitions 
(metadata)

![image](https://github.com/user-attachments/assets/b6056ef0-d49e-496b-b323-8f896ba1d984)

---

## Zookeeper

Kafka cannot work without Zookeeper.
Same goes for HBase.
 Zookeeper manages brokers (keep a list of them)
 Zookeeper helps in performing leader election for partitions
 Zookeeper sends notification to Kafka in case of changes (e.g
new topic, broker dies, broker comes up, delete topics…)
 Kafka cannot work without Zookeeper
 Zookeeper by design operates with an odd number of servers (3, 
5, 7)
 Zookeeper has a leader (handle writes) the rest of the servers 
are followers (handle reads)
 Zookeeper does not store consumer offsets with Kafka > v0.10

![image](https://github.com/user-attachments/assets/b2fe444f-33db-4767-a76f-8863c1ec89a4)

---

## Kafka guarantees
 Messages are appended to a topic-partition in the order they are 
sent
 Consumers read messages in the order stored in a topic-partition
 With a replication factor of N, producers and consumers can 
tolerate up to N-1 brokers being down
 This is why a replication factor of 3 is a good idea:
 Allows for one broker to be taken down for maintenance
 Allows for another broker to be taken down unexpectedly
 As long as the number of partitions remains constant for a topic 
(no new partitions), the same key will always go to the same 
partition

---

## Theory roundup

![image](https://github.com/user-attachments/assets/4a8fb287-23f8-49ea-a7d9-663d85939b55)















