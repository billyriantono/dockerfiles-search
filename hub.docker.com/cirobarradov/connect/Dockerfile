FROM confluentinc/cp-kafka-connect

ADD kafka-connect-elasticsearch-3.1.0-SNAPSHOT.jar /usr/share/java/kafka/
ADD jjjjeest-jest-2.0.4-SNAPSHOT.jar /usr/share/java/kafka/
RUN rm /usr/share/java/kafka-connect-hdfs/httpcore-4.2.4.jar
RUN rm /usr/share/java/kafka-connect-hdfs/httpclient-4.2.5.jar

#ADD kafka-connect-elasticsearch-3.1.0-SNAPSHOT-jar-with-dependencies.jar /usr/share/java/kafka/
#RUN rm /usr/share/java/kafka/httpclient-4.5.1.jar
#RUN rm /usr/share/java/kafka/httpmime-4.5.1.jar
#RUN rm /usr/share/java/kafka/httpcore-4.4.3.jar
