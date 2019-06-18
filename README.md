# kafkaConnect-jdbc-connector-sql
Connect SQL server using JDBC connector

#Connect Sql Server using kafka connect and jdbc connector

to run this example you need to have SQL server installed.


and then follow the steps to start

1. start zookeeper server

	kafka_2.12-2.2.1/bin/zookeeper-server-start.sh zookeeper.properties

2. then start kafka server

	kafka_2.12-2.2.1/bin/kafka-server-start.sh server.properties

3. register the connector

	kafka_2.12-2.2.1/bin/connect-standalone.sh connect-standalone.properties sql-server-jdbc-connector.properties

	table.whitelist - specify tables you want to monitor
	mode - specifiy the mode incrementing, timestamp, both
	for more - https://docs.confluent.io/current/connect/kafka-connect-jdbc/source-connector/source_config_options.html#mode

4. check topic list

	kafka_2.12-2.2.1/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list

	and check wheather there are any topics starting from "incrementing-" 
	* you can change the prefix by changing topic.prefix in connector properties

5. start console consumer and subscribe to a topic

	kafka_2.12-2.2.1/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --from-beginning --topic incrementing-students

6. make changes (insert, update) and see those are reflected on consumer.
