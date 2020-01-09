FROM java:8

MAINTAINER architecture@datiobd.com

#Install and update functionality
RUN apt-get update
RUN apt-get install wget

#Download microservice
RUN wget https://s3-eu-west-1.amazonaws.com/work-gaspi/kafka-stream-1.0-SNAPSHOT-bin.tar.gz && tar -xvf kafka-stream-1.0-SNAPSHOT-bin.tar.gz

#Execute microservice
WORKDIR /kafka-stream-1.0-SNAPSHOT/bin/
ENTRYPOINT ./Main
