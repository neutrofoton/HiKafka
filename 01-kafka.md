
# Message Broker vs Message Queue

**Message Broker** - A  message-oriented middleware (messaging system) server that hosts messaging destinations (i.e., queues and topics) for the purposes of asynchronous communication. Sometimes known as a queue manager.

Example implementation of Message Broker is communication among services on microservice architecture. 

**Message Queue** - A messaging destination mechanism that uses a queue data structure to hold messages and is hosted by the message broker. The alternative to a queue is a topic which provides publish/subscribe semantics.

Example implementatoin of Message Queue is notification service on an application.

https://coderanch.com/t/521364/java/Message-Queue-Message-Broker

# Apache Kafka
Apache Kafka is distributed publish-subscribe messaging system. The publishers publish messages, meanwhile the subscribers receive/consume the messages.

In real life example, youtube is an example of publish subscriber system. The video creators are publishers, meanwhile the viewers/subscribers are subscribers which watch the published videos. Youtube stores published videos and can be watched by viewers any time. 

# Broker
As describing previously, Kafka is a publish-subscribe messaging system. In every publish-subscribe messaging system, messages are store somewhere. The **publisher (producer)** sends messages to the somewhere, and the **subscriber (consumer)** receives/reads the message from the somewhere. In Kafka, the **broker** is responsible for that operation. 

The responsibilities of broker are:

1. Giving ability for producers to send messages
2. Storing those messages
3. Giving ability for consumers to read those messages

Kafka broker simply stores messages on files.

<image src="images/kafka-simple-pub-sub.png"/>  
<p></p>


<image src="images/kafka-multiple-pub-sub.png"/>  

In a single phisical server, we may run multiple Kafka broker. We may even create a Kafka cluster on a single computer.

<image src="images/kafka-broker-cluster.png"/>  

Since broker stores the messages, that's why to avoid whole system is down commonly we apply kafka cluster on production. If one broker is down, other broker can still handle message transmission. 

On broker cluster, producers may send messages to different Kafka brokers. It means that messages from different producers will be spread among different broker or even different servers. By that condition, the consumers may read messages from multiple brokers or even different server.

How the brokers synchonize each others, distributed load, etc is managed by Zookeeper.

# Kafka Installation
```bash
curl -o ~/workspace/learn-kafka/kafka.tgz https://downloads.apache.org/kafka/3.6.0/kafka_2.13-3.6.0.tgz

tar -xvzf kafka.tgz
cd kafka_2.13-3.6.0 
```

## Zookeeper
``` bash
# starting zookeeper by passing zookeeper configuration
bin/zookeeper-server-start.sh config/zookeeper.properties

```
``` text
# output
....
....

INFO binding to port 0.0.0.0/0.0.0.0:2181 (org.apache.zookeeper.server.NIOServerCnxnFactory)
....
....

```

At the <code>config/zookeeper.properties</code> is the location zookeeper configuration.

```bash
....
....

# location of zookeeper store data
dataDir=/tmp/zookeeper

# the port at which the clients will connect
clientPort=2181

....
....
```

## Kafka Server

When start kafka, we need to keep zookeeper running
```bash
# starting kafka serer
bin/kafka-server-start.sh config/server.properties

```

``` text
# output:
....
....
INFO starting (kafka.server.KafkaServer)
INFO Connecting to zookeeper on localhost:2181 (kafka.server.KafkaServer)
INFO [ZooKeeperClient Kafka server] Initializing a new session to localhost:2181. (kafka.zookeeper.ZooKeeperClient)
....
....
INFO Opening socket connection to server localhost/127.0.0.1:2181. (org.apache.zookeeper.ClientCnxn)
INFO Socket connection established, initiating session, client: /127.0.0.1:41022, server: localhost/127.0.0.1:2181 (org.apache.zookeeper.ClientCnxn)
INFO Session establishment complete on server localhost/127.0.0.1:2181, session id = 0x100002a59dc0000, negotiated timeout = 18000 (org.apache.zookeeper.ClientCnxn)
INFO [ZooKeeperClient Kafka server] Connected. (kafka.zookeeper.ZooKeeperClient)
....
....
INFO KafkaConfig values: 
....

listeners = PLAINTEXT://:9092
....
....
INFO [ThrottledChannelReaper-ControllerMutation]: Starting (kafka.server.ClientQuotaManager$ThrottledChannelReaper)
INFO Log directory /tmp/kafka-logs not found, creating it. (kafka.log.LogManager)
INFO Loading logs from log dirs ArraySeq(/tmp/kafka-logs) (kafka.log.LogManager)
INFO No logs found to be loaded in /tmp/kafka-logs (kafka.log.LogManager)
...
...
INFO [MetadataCache brokerId=0] Updated cache from existing None to latest Features(version=3.6-IV2, finalizedFeatures={}, finalizedFeaturesEpoch=0). (kafka.server.metadata.ZkMetadataCache)
INFO [TxnMarkerSenderThread-0]: Starting (kafka.coordinator.transaction.TransactionMarkerChannelManager)
...
...
INFO [KafkaServer id=0] started (kafka.server.KafkaServer)
....
....
```

The kafka server configuration located on <code>config/server.properties</code>.
```bash
...
...
# The id of the broker. This must be set to a unique integer for each broker.
broker.id=0
....
...
# A comma separated list of directories under which to store log files
log.dirs=/tmp/kafka-logs # location where kafka store messages.
...
...
zookeeper.connect=localhost:2181
```