# Large table splitting smooth migration steps

## Whole process
> The overall process is divided into 4 steps.As follows:

![Large table splitting smooth migration steps](../Material/image/Large%20table%20splitting%20smooth%20migration%20steps%20—%20Whole%20Process.png)

## Detail
### Stock data migration

* Xtrabackup is used to generate data snapshots to new tables

* The current data offset is recorded in preparation for incremental synchronization

### Incremental data migration

* Cancel is used to monitor binlog logs and it send message to Kafka

* Consuming Kafka messages is equivalent to completing the synchronization of incremental data

### Data verifying program

### Program double writing

### Program query switch

