# Consuming Kafka Message

## Consuming Realtime Message
Kafka also provide a consumer executable file which demonstrate how to receive message sent by a Kafka message producer.

```bash
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic cities
```

Once we run the <code>kafka-console-consumer.sh</code>, the aplication will show empty and try to listen to any new message that sent by the Producer. 

If we send a new message from producer, the message will automatically received and displayed on the consumer side.
Thus, we need to run both the producer and consumer (on seperated terminal tab).

## Consuming From Beginning and Realtime Message

```bash
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic cities --from-beginning
```

The above command will show all message start from the beginning. Then new incoming realtime message will be received as well, as long the application (terminal command) not terminated.

# Conclusion
- Producers send message to Kafka, consumers receive messages from Kafka.
- Multiple producers and multiple consumers may connect to the same Kafka cluster.
- Kafka stores messages even they were already consumed by one of the consumers.
- Same messages may be read multiple times by different consumers (example read from beginning).
- The producers and consumers which connect to Kafka cluster are independent each others. They may connect or disconnect (close) any time without interupting one another.
