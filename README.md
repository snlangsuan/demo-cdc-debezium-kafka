# Change Data Capture with Debezium and Kafka

Change Data Capture with Debezium and Kafka based on Docker

## Getting Started

### Installing

1. Clone this repository anywhere on your machine:
   
  ```sh
  $ get clone https://github.com/snlangsuan/demo-cdc-debezium-kafka.git
  ```

2. Run docker compose build

```sh
  $ docker-compose up -d
```

### Usage

1. Access to MariaDB

```sh
$ docker-compose -f docker-compose.yml exec mariadb \
    bash -c 'mysql -uroot -p$MYSQL_ROOT_PASSWORD inventory'
```

2. Register a connector to monitor the database

```sh
$ curl -i -X POST \
    -H 'Accept: application/json' \
    -H 'Content-Type: application/json' \
    -d @register-mysql.json \
    http://localhost:8083/connectors
```

3. Display list of connectors

```sh
$ curl http://localhost:8083/connectors
```

4. Get a connector by name

```sh
$ curl http://localhost:8083/connectors/inventory-connector
```

5. Delete a connector by name

```sh
$ curl -X DELETE http://localhost:8083/connectors/inventory-connector
```

6. Get a list of topics

```sh
$ docker-compose run --rm kafka list-topics
```

7. Watch topic by topic name

```sh
$ docker-compose run --rm kafka watch-topic \
    -a -k 'dbserver1.inventory.customers'
```

## Acknowledgments
- [Debezium Tutorial](https://debezium.io/documentation/reference/tutorial.html)
- [Elasticsearch Service Sink Connector for Confluent Platform](https://docs.confluent.io/current/connect/kafka-connect-elasticsearch/index.html)