# Download Kafka
```bash
curl -o ~/workspace/learn-kafka/kafka.tgz https://downloads.apache.org/kafka/3.6.0/kafka_2.13-3.6.0.tgz

tar -xvzf kafka.tgz
cd kafka_2.13-3.6.0 
```

# Zookeeper
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

# Kafka Server

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