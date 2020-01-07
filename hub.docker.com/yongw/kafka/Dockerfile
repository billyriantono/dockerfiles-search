FROM yongw/java-1.8

MAINTAINER Yong Wang <yongw@live.com>


ENV KAFKA_VERSION="0.10.1.0" SCALA_VERSION="2.11"

# Download and extract Kafka
RUN curl --silent --retry 3 \
    http://mirrors.tuna.tsinghua.edu.cn/apache/kafka/$KAFKA_VERSION/kafka_$SCALA_VERSION-$KAFKA_VERSION.tgz \
    | tar xz -C /opt

ADD docker-entrypoint.sh /
RUN chmod a+x /docker-entrypoint.sh

EXPOSE 9092
EXPOSE 2181

VOLUME ["/kafka/log"]

ENV KAFKA_HOME /opt/kafka_${SCALA_VERSION}-${KAFKA_VERSION}

WORKDIR ${KAFKA_HOME}

CMD ["/docker-entrypoint.sh"]
