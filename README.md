# Kafka-Windows-Setup
The read-me file contains step by step information to setup Kafka in your Windows OS machine

Download and extract the latest Kafka release. Store the file in C drive where you have either /"Program Files"/Java or /Java installed.
Open command prompt and reach to kafka folder location (C:\kafka_2.13-3.7.0)

For starting the kafka environment, we can either use ZooKeeper or kRaft. I have used ZooKeeper service.
Apache Zookeeper is a free open source service which helper Apache Kafka to manage multiple servers in a distributed environment. ZooKeeper have the following roles.
Tracking broker membership
Managing topic configuration
Storing meta data
Selecting leader in case of partition failure
Notifying broker of changes
Distributing data across multiple partitions
Enable failover migration
Storing access control list
Brokers follows Master Slave architecture so whenever there is a failure of a node, a new master is elected by zookeeper.

  First we start ZooKeeper service using :

   	.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
   
  Once the zookeeper service has started, we initialize kafka server using:

   	.\bin\windows\kafka-server-start.bat .\config\server.properties

  Now we have both ZooKeeper service and Kafka Server running

Let's create a topic.
Topic is like a folder to divide the events pushed in kafka into categories. The topic can be partitioned and each partition is present in a different broker/server. Each partition     of a topic can be replicated one or more times in order to maintain fault tolerance in case of any failure.
   
While creating a topic, we can define these properties of number of partitions and number of replications. As this is a setup on local, we will have one partition and one replication.

  We can create topic using command
    
    .\bin\windows\kafka-topics.bat --create --topic demoTopic --partitions 1 -- replication-factor 1 --bootstrap-server localhost:9092


Once a topic is created, we can now produce/consume data from this topic.
  To produce data, we can create a console producer in a new console using : 
    
    .\bin\windows\kafka-console-producer.bat --topic demoTopic --bootstrap-server localhost:9092
   
  To consumer data, we can create a console consumer in a new console using : 
  
    .\bin\windows\kafka-console-consumer.bat --topic demoTopic --bootstrap-server localhost:9092

As soon as we add any line in our producer console, the line will be visible in consumer console. This marks the completion of kafka setup on windows. 
You can play with kafka stream to process the event streams and with Kafka Connect to create producer and consumer connectors to help you ingest data continously from existing data source

