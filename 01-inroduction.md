
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

How the brokers synchonize each others, distributed load, etc is managed by **Zookeeper**.


# Kafka Package Installer
```bash
curl -o ~/workspace/learn-kafka/kafka.tgz https://downloads.apache.org/kafka/3.6.0/kafka_2.13-3.6.0.tgz

tar -xvzf kafka.tgz
cd kafka_2.13-3.6.0 
```
