# Generic Kafka Event Producer

### Overview
This application will provide REST endpoints to publish kafka messages with following value encodings.
   - AVRO
   - JSON

Users can set following parameters in the kafka message.
   - Topic
   - Headers(any number of key-value pairs)
   - Key(kafka message key)
   - Value(kafka message payload)

### Running the application
#### Build the docker image
```sh 
   docker build -f Dockerfile -t generic-producer .
```

#### Pull the repository image
```sh
   docker pull wgarunap/generic-kafka-event-producer:v1.1.0
```

#### Run generic event producer
```sh
docker run -dit -e SCHEMAREG_URL=http://schemareg.event.com:8081 -e KAFKA_BROKERS=kafka-1:9092,kafka-2:9092 -p 8000:8000 wgarunap/generic-kafka-event-producer:v1.1.0
```

### Configs 
```sh
   // Schema registry url to fetch the avro event schemas 
   SCHEMAREG_URL=http://schemareg.event.com:8081

   // kafka brokers list
   KAFKA_BROKERS=kafka-1,kafka-2,kafka-2

   // http serving port
   PORT=8000
```

### Avro Producer 
#### Request URL
```sh
   <HOST>:<PORT>/publish/avro
```
#### Example POST Request Payload
```json
{
   "topic":"test",
   "subject":"com.event.EventName",
   "version":2,
   "headers":{
      "key1":"value1",
      "key2":"value2",
   },
   "key":"test",
   "value":{
      "meta":{
         "event_id":"123e4567-e89b-12d3-a456-426655440000",
         "trace_id":"123e4567-e89b-12d3-a456-426655440000",
         "account_id":"123e4567-e89b-12d3-a456-426655440000"
      }
   }
}
```

### JSON Producer 
#### Request URL
```sh
   <HOST>:<PORT>/publish/json
```
#### Example POST Request Payload
```json
{
   "topic":"test",
   "headers":{
      "account_id":"123e4567-e89b-12d3-a456-426655440000"
   },
   "key":"test",
   "value":{
      "meta":{
         "event_id":"123e4567-e89b-12d3-a456-426655440000",
         "trace_id":"123e4567-e89b-12d3-a456-426655440000",
         "account_id":"123e4567-e89b-12d3-a456-426655440000"
      }
   }
}
```

### Null Producer 
#### Request URL
```sh
   <HOST>:<PORT>/publish/null
```
#### Example POST Request Payload
```json
{
   "topic":"test",
   "headers":{
      "subject":"com.event.EventName",
      "account_id":"123e4567-e89b-12d3-a456-426655440000"
   },
   "key":"test",
}
```


### TODO
   - Add Key encoding methods
   - Add following key/value encoding methods
      - Binary
      - String
      - Protobuf
      - MessagePack
   - Add authentication layer
   - 
      