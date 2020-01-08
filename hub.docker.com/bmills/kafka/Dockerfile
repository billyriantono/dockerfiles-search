FROM alpine

#install dependencies
RUN apk update
RUN apk add bash openjdk7

#set working directory
WORKDIR /root/

#get kafka
RUN wget http://apache.claz.org/kafka/0.8.2.2/kafka_2.11-0.8.2.2.tgz && \
    tar -xzf kafka_2.11-0.8.2.2.tgz && \
    rm -f kafka_2.11-0.8.2.2.tgz

WORKDIR /root/kafka_2.11-0.8.2.2/
#add our custom config and sh script
ADD ./src ./config
ADD startKafka.sh ./
RUN chmod 777 startKafka.sh

#run the server
CMD ./startKafka.sh



