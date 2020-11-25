## zookeeper and kafka
原文链接: https://blog.csdn.net/wchyumo2009/article/details/88965053

### network
```sh
docker network create --driver bridge --subnet 172.23.0.0/25 --gateway 172.23.0.1  zookeeper_network
```

### 1, 查看zookeeper集群是否正常
docker exec -it zoo1 bash
bin/zkServer.sh status # mode 为leader或follower正常

### 2, 创建topic
#### 验证，每个list理论上都可以看到新建的topic
docker exec -it kafka1 bash
kafka-topics.sh --create --zookeeper zoo1:2181 --replication-factor 1 --partitions 3 --topic test001
kafka-topics.sh --list --zookeeper zoo1:2181
kafka-topics.sh --list --zookeeper zoo2:2181
kafka-topics.sh --list --zookeeper zoo3:2181

#### 生产消息
kafka-console-producer.sh --broker-list kafka1:9092,kafka2:9093,kafka3:9094 --topic test001

#### 消费消息
kafka-console-consumer.sh --bootstrap-server kafka1:9092,kafka2:9093,kafka3:9094 --topic test001 --from-beginning

### 
