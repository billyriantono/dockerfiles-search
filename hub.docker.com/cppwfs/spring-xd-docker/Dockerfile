#####################################################
# Docker File for Sandbox XD Image
#####################################################
FROM ubuntu
MAINTAINER Glenn Renfro
#Update 
RUN apt-get update
#Install Tools 
RUN apt-get -y install openjdk-7-jre-headless
RUN apt-get -y install erlang
RUN apt-get -y install wget
RUN sudo apt-get install erlang
RUN sudo apt-get install unzip
RUN apt-get -y install make
RUN apt-get -y install build-essential
# Install Rabbit
RUN wget https://www.rabbitmq.com/releases/rabbitmq-server/v3.3.5/rabbitmq-server-generic-unix-3.3.5.tar.gz
RUN tar -xvf rabbitmq-server-generic-unix-3.3.5.tar.gz
#Install Spring XD
RUN wget https://repo.spring.io/libs-snapshot/org/springframework/xd/spring-xd/1.0.1.BUILD-SNAPSHOT/spring-xd-1.0.1.BUILD-SNAPSHOT-dist.zip
RUN unzip spring-xd-1.0.1.BUILD-SNAPSHOT-dist.zip
#Install Redis
RUN wget http://download.redis.io/releases/redis-2.8.17.tar.gz
RUN tar xzf redis-2.8.17.tar.gz
RUN make -C /redis-2.8.17
# Setup Ports
EXPOSE 9393
#setup ENV
ENV spring_redis_address localhost:6379
ENV spring_rabbitmq_addresses localhost:5672
ENV XD_TRANSPORT rabbit
#Setup RunFile
RUN echo "#!/bin/bash" >runAll.sh
RUN echo "/redis-2.8.17/src/redis-server &" >>runAll.sh
RUN echo "/rabbitmq_server-3.3.5/sbin/rabbitmq-server & ">>runAll.sh
RUN echo "sleep 5 ">>runAll.sh
RUN echo "/spring-xd-1.0.1.BUILD-SNAPSHOT/xd/bin/xd-singlenode  --analytics redis  "  >>runAll.sh
RUN chmod +x runAll.sh
CMD ./runAll.sh &
