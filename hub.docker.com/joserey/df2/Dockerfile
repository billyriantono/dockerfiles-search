FROM openjdk:8

CMD wget http://apache.cs.uu.nl/spark/spark-2.3.0/spark-2.3.0-bin-hadoop2.7.tgz
CMD tar -xf spark-2.3.0-bin-hadoop2.7.tgz
CMD rm spark-2.3.0-bin-hadoop2.7.tgz

CMD wget http://apache.cs.uu.nl/cassandra/3.11.2/apache-cassandra-3.11.2-bin.tar.gz
CMD tar -xf apache-cassandra-3.11.2-bin.tar.gz
CMD rm apache-cassandra-3.11.2-bin.tar.gz

CMD wget http://apache.redkiwi.nl/kafka/1.1.0/kafka_2.11-1.1.0.tgz
CMD tar -xf kafka_2.11-1.1.0.tgz


CMD pwd
CMD ls

CMD spark-2.3.0-bin-hadoop2.7/bin/spark-shell.sh
