From the previous section we get, default cofiguration
|Server         |Address        |
|:---           | ---           |
|Zookeper       | localhost:2181|
|Kafka (broker) | localhost:9092|

> If we want to run multiple kafka server/broker on a computer, of course we need to set different port for each.

# Creating Kafka Topic
To demonstrate creating kafka topic, we can use script which shipped with kafka binary distribution.
```bash
# creating kafka a topic (called cities)
bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic cities

# output
Created topic cities.
```

After creating the kafka topic: <code>cities</code>, kafka will generate a folder in the kafka logs directory. In this example named <code>cities-0</code>

In the kafka server configuration <code>server.properties</code>, there is definition:

```bash
...
...

# The default number of log partitions per topic. More partitions allow greater
# parallelism for consumption, but this will also result in more files across
# the brokers.
num.partitions=1

...
...

```

Since we do not specify number of partition, kafka will set the number of partion to 1 (based on configuration).
The number of partion we apply which causes kafka generating topic directory with suffix 0 (<code>cities-0</code>).  

<image src="images/kafka-topic-cities.png"/>  

In kafka, messages can be spread in several partition. Every partion basically folders as we got <code>cities-0</code>).
If we set the number of partion to 2, we will get <code>cities-0</code>, <code>cities-1</code>.

# Read Kafka Topic
To read the list of kafka topic we can use the script shipped with kafka binary distribution
```bash
bin/kafka-topics.sh --bootstrap-server localhost:9092 --list 
```