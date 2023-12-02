# Message Storage

Location of Kafka storing message defined on the <code>server.properties</code>.
```bash
...
log.dirs=/tmp/kafka-logs
...

```

> Kafka does not store all message forever. After specific amount of time (or when size of the log exceeds configured max size), the messages are deleted. The default log retention period is 7 days (168 hours)