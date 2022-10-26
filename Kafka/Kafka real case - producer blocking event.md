# Kafka real case - producer blocking event

## 1. Background

1. 2021-12-07 16:00 Beijing time, running batch tasks
2. The server memory decreased sharply, and then ZK and Kafka committed suicide one after another
3. kafka message sending failed and blocking normal function

## 2. Check

There are 3 nodes in zk deployment. 

Although the original leader of zk has died, it can be observed from the log that a new leader has been newly elected, and the suspicion can be ruled out temporarily.

Then, we turn our attention to kafka.

reason:
1. When the memory of the Linux machine is insufficient, the process that occupies the most memory will be killed first, so kafka is killed
2. The partition of the test service topic is not redundant, and it is not really high availability.




