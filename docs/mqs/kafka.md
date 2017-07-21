# Kafka

Apache Kafka is a distributed streaming platform. We think of a streaming platform as having three key capabilities:

1. It lets you publish and subscribe to stream of records.
2. It lets you store streams of records in a fault-tolerant way.
3. It lets you process streams of records as they occur.

First a few concepts:

* Kafka is run as a cluster on one or more servers.
* The Kafka cluster stores streams of records in categories called topics.
* Each record consists of a key, a value, and a timestamp.


## Installation

#### Download the code

Download the [kafka](http://mirror.bit.edu.cn/apache/kafka/0.11.0.0/kafka_2.11-0.11.0.0.tgz) and un-tar it

    $ tar -zxf kafka_*.tgz

#### Start the server

Kafka uses [zookeeper](http://mirrors.cnnic.cn/apache/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz) so you need to first
start a zookeeper server if you don't already have one. You can use the convenience script packaged with kafka to get
a quick-and-dirty single-node zookeeper instance.

    $ zookeeper-server-start.sh config/zookeeper.properties

Now start the kafka server

    $ kafka-server-start.sh config/server.properties

#### Create a topic

Let's create a topic named "test" with a single prtition and only one replica:

    $ kafka-topics.sh --create --zookeeper localhost:2128 --replication-factor 1 --partitions 1 --topic test

We can now see the topic if we run the list topic cammand:

    $ kafka-topics.sh --list --zookeeper localhost:2128

    test

Alternatively,instead of manaually creating topics you can also configure your brokers to auto-create topics.
