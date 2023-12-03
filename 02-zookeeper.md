
The main responsibilities of zookeeper in Apache Kafka cluster are:
1. Maintaining list of active brokers
2. Electing controller. The contoller is elected among broker in the cluster.
3. Managing configuration of topics and partions


<image src="images/zookeeper.png"/>  

Since zookeeper is mandatory component in Kafka cluster, it is recommended to have more than one zookeeper (zookeeper cluster) in the Kafka cluster. It is also recommeded odd number of zookeeper in the cluster.

<image src="images/zookeeper-cluster.png"/>  

<image src="images/zookeeper-bad-design.png"/>  

<p></p>

# Running Zookeeper
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
