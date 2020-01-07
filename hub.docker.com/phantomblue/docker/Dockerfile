FROM anapsix/alpine-java
MAINTAINER Rui Wang <phantomblue@126.com>

RUN apk add --update bash zip curl && \
    curl http://www.us.apache.org/dist/kafka/0.9.0.1/kafka_2.11-0.9.0.1.tgz| tar -xzf - && \
    mv kafka_2.11-0.9.0.1 /kafka && \
    rm /var/cache/apk/*
RUN mkdir /tmp/zookeeper
RUN mkdir /tmp/kafka-logs
VOLUME ["/data"]
ENV KAFKA_HOME /kafka
ENV PATH /kafka:$PATH
WORKDIR /kafka
ADD run.sh /kafka/run.sh
RUN chmod a+x /kafka/run.sh
EXPOSE 9092
EXPOSE 2181   
CMD ["/kafka/run.sh"]
