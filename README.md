# Connect SQL server using JDBC, Debezium connectors

##### to connect using debezium connetor
 - need to enable CDC of sql server and for the tables you wish to track 

  to run this example you need to have SQL server installed.

#### 1. start zookeeper server.
```sh
$ kafka_2.12-2.2.1/bin/zookeeper-server-start.sh zookeeper.properties
```
####  2. start kafka server
```sh
$ kafka_2.12-2.2.1/bin/kafka-server-start.sh server.properties
```
####  3. register the connector
```sh
$ kafka_2.12-2.2.1/bin/connect-standalone.sh connect-standalone.properties sql-server-jdbc-connector.properties
```
	- table.whitelist - specify tables you want to monitor
	- mode - specifiy the mode incrementing, timestamp, both

####  4. check topic list
```sh
$ kafka_2.12-2.2.1/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```
	- and check whether there are any topics starting from "incrementing-" 
	* you can change the prefix by changing topic.prefix in connector properties

####  5. start console consumer and subscribe to a topic
```sh
$ kafka_2.12-2.2.1/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic incrementing-students
```
####  6. make changes (insert, update) and see those are reflected on consumer.

