# Consuming Kafka Message

Kafka also provide a consumer executable file which demonstrate how to receive message sent by a Kafka message producer.

```bash
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic cities
```

Once we run the <code>kafka-console-consumer.sh</code>, the aplication will show empty and try to listen to any new message that sent by the Producer. 

If we send a new message from producer, the message will automatically received and displayed on the consumer side.
Thus, we need to run both the producer and consumer (on seperated terminal tab).