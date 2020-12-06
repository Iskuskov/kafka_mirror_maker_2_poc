# Proof of Concept for MirrorMaker 2.0 
_Docker compose playground for Kafka MirrorMaker 2.0_

1. Start containers:
`docker-compose up`

2. Create topic in source cluster:
```sh
docker-compose exec srcKafka1 kafka-topics \
  --create \
  --bootstrap-server localhost:9092 \  
  --replication-factor 1  
```

3. Consume messages in target cluster:
```sh
docker-compose exec kafkacat kafkacat -b destKafka1:11091 -C -t users 
```

4. Produce messages from source cluster:
```sh
docker-compose exec kafkacat kafkacat -b srcKafka1:10091 -P -t users
```
