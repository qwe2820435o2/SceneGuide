
# Link Design

## 1. Behavior Collecting

```markdown
Behavior burying interface requests a lot

In addition to simply verifying the accuracy of the data here, the information should be directly sent to the big data Kafka
```

## 2. Business Collecting

```markdown
Due to the characteristics of the business buried point, secondary forwarding after processing is required here

The information is first sent to RabbitMQ, processed by its consumers, and then the data is sent to the big data Kafka
```





