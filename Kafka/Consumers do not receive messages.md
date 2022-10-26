# Consumers do not receive messages

**Reason：**

The client version is inconsistent with the server version

**Solution:**

I use the server here: kafka_2.10-0.8.2.1.tgz, the client used 0.8.1 originally, it needs to be changed to:

```shell script
<dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka_2.9.2</artifactId>
        <version>0.8.2.1</version>
</dependency>
```


When using kafka, it should be noted that the version of the kafka client (kafka-client) must correspond to the version of the kafka server.

Otherwise, the message sending will fail.