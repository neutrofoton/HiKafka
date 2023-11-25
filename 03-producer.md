# Sending Message to Kafka

Kafka binary provide a producer message called <code>bin/kafka-console-producer.sh </code>. We can run the executable then type message to simulate sending message to Kafka.

```bash
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic cities
```

```text
# Output: It will show prompt so that we can enter message

> Jakarta
> Surabaya
```