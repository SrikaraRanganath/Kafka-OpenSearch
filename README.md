﻿# Kafka-Wikimedia-OpenSearch
 
This application uses a Apache Kafka Cluster (v<4.0) with three partitions and a replication factor of 2 to ensure fault tolerance and availability. It consists of 
+ Producer - Wikimedia data stream which consists of the changes being made in all the channels under wiki
* Consumer - It is a OpenSearch application running on the cloud provider *bonsai* and uses REST API to send the data across. (https://bonsai.io/blog/up-and-running-with-opensearch)

## Configuration 
1. The producer is **idempotent** as it proccesses the data in batches and the default configuration for the Kafka Cluster is *Round-Robin*, however we can attach keys to the messages so that it gets stored under their respective partition.
2. The provider is linked to this data stream https://stream.wikimedia.org/v2/stream/recentchange
3. It uses a String for serialization and deserialization

## Dependency
This application runs on all versions of Apache Kafka < 4.0 as it has Apache Zookeeper as a dependency and it cannot work on Kraft alone.

## Running the Kafka Cluster
1. Start zookeeper with default config
```
zookeeper-server-start.sh ~/kafka_2.13-3.2.3/config/zookeeper.properties
```
2. Start kafka with default config
```
kafka-server-start.sh ~/kafka_2.13-3.2.3/config/server.properties
```

