FROM java:openjdk-8-jre-alpine

ENV ZOOKEEPER_VERSION 3.4.8
LABEL name="zookkeeper" version="${ZOOKEEPER_VERSION}"

RUN apk add --no-cache wget bash && \
    cd / && \
    mkdir zk && \
    wget -q -O - http://apache.mirrors.pair.com/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz | tar xfz - -C zk && \
    mv /zk/zookeeper-${ZOOKEEPER_VERSION} / &&  \
    rm -rf zk && \
    mkdir -p /data/zookeeper

COPY zoo.cfg /zookeeper-${ZOOKEEPER_VERSION}/conf
COPY entrypoint.sh /entrypoint.sh

RUN chown -R nobody:nobody /entrypoint.sh /data/ /zookeeper-${ZOOKEEPER_VERSION}

EXPOSE 2181 2888 3888

USER nobody
ENTRYPOINT ["/entrypoint.sh"]
CMD /zookeeper-${ZOOKEEPER_VERSION}/bin/zkServer.sh start-foreground
