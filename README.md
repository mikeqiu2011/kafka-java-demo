# java kafka docker demo

## run docker
    docker-compose up -d
    
## explore kafka
    docker exec -it kafka-broker bash
    ls /opt/bitnami/kafka/config
    ls /opt/bitnami/kafka/logs
    ls /opt/bitnami/kafka/bin

## create topic
    ./kafka-topics.sh \
            --create \
            --topic kafka.learning.tweets \
            --partitions 1 \
            --replication-factor 1 \
            --zookeeper zookeeper:2181

    ./kafka-topics.sh \
        --zookeeper zookeeper:2181 \
        --create \
        --topic kafka.learning.alerts \
        --partitions 1 \
        --replication-factor 1

    ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --list

## Getting details about a Topic

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --describe


## Publishing Messages to Topics

        ./kafka-console-producer.sh \
            --broker-list kafka:9092 \
            --topic kafka.learning.tweets

## Consuming Messages from Topics

        ./kafka-console-consumer.sh \
            --bootstrap-server kafka:9092 \
            --topic kafka.learning.tweets \
            --from-beginning

## Deleting Topics

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --delete \
            --topic kafka.learning.alerts




## check zookeeper
    docker exec -it zookeeper bash
    cd /opt/zookeeper-3.4.6/bin/
    ./zooCli.sh
    ls /brokers/ids
    get /brokers/ids/1002



#Create a Topic with multiple partitions

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --create \
            --topic kafka.learning.orders \
            --partitions 3 \
            --replication-factor 1


#Check topic partitioning

        ./kafka-topics.sh \
            --zookeeper zookeeper:2181 \
            --topic kafka.learning.orders \
            --describe

## Publishing Messages to Topics with keys

        ./kafka-console-producer.sh \
            --broker-list kafka:9092 \
            --property "parse.key=true" \
            --property "key.separator=:" \
            --topic kafka.learning.orders

## Consume messages using a consumer group

        ./kafka-console-consumer.sh \
            --bootstrap-server kafka:9092 \
            --topic kafka.learning.orders \
            --group test-consumer-group \
            --from-beginning

## Check current status of offsets

        ./kafka-consumer-groups.sh \
            --bootstrap-server localhost:29092 \
            --describe \
            --all-groups

