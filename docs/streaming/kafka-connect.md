# Kafka Connect

Apache Kafka 101: Kafka Connect
https://www.youtube.com/watch?v=J6adhl3wEj4
Dec 17, 2020

- Kafka Connect, also known as Apache Kafka's integration API

- it is 2 things
  - an ecosystem of pluggable conenctors
  - a client application used to get data into Kafka from external systems, and out of external systems into Kafka
  
Used for data integration.

To a Kafka cluster, Connect looks like a Producer, or a Consumer (or both). Everything that is not a broker in Kakfa is one of those things. 

Connect is a process that runs on hardwarre independent of the brokers themselves.

- scalable and fault tolerant
- can be a cluster of Connect workers

A Connector abstracts the data integration specifics, only some JSON configuration is required to run the Connector. 

eg. streaming to ElasticSearch
  Subscribes to a topic, gets messages, uses the ElasticSearch API. 

Connector - is a pluggable component (interfaces with the external system) - this basically a JAR file (which contains the JVM Connect code within it).

Connector - also has a runtime sense. The JSON is submitted to the REST endpoint on the Connect cluster which runs the Connect code. The JAR becomes instantiated which runs on a Connect worker (one of the nodes in the cluster). 

A "source" connector, reads from an external system and acts as a Kafka Producer.
A "sink" connector, subscribes to a Kafka topic and writes to the external system.

Each connector is either a source or a sink. The Kafka cluster only sees a producer (source connector) or a consumer (sink coneector). 

Advantage of Connect - it is an ecosytem, others have written the code to integrate with specific systems. This code is likely to be very similar across companies - it is undifferentiated code. It is not likely to add any kind of unique value to you. 

The Confluent Hub confluent.io/hub. Has a command line tool. But Connectors don't need to be on the Hub.  

The Connect API is straightforward, the difficulty of writing a Connector is in integrating with the external system depending on what options that interface has.

Connect is a fairly complex distributed system in its own right. Plus the value of the plugin ecosystem is high.

eg. reading from a relational database. Need to keep track of the last ID you saw. Need to store that state somewhere. What happens when that Connect worker fails, how is that state retained, picked up by a new worker. 


