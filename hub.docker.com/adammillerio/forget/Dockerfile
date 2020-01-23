FROM adambrown/java:0.1.0

RUN \
    grep '^networkaddress.cache.ttl=' /usr/lib/jvm/java-7-oracle/jre/lib/security/java.security || \
    echo 'networkaddress.cache.ttl=60' >> /usr/lib/jvm/java-7-oracle/jre/lib/security/java.security && \
    wget -O /tmp/zookeeper.tgz http://www.apache.org/dist/zookeeper/zookeeper-3.4.6/zookeeper-3.4.6.tar.gz && \
    mkdir -p /opt/zookeeper/transactions /opt/zookeeper/snapshots && \
    tar -xzf /tmp/zookeeper.tgz -C /opt/zookeeper --strip=1 && \
    rm /tmp/zookeeper.tgz && \
    mkdir -p /opt/exhibitor && \
    wget -O /opt/exhibitor/exhibitor.jar http://central.maven.org/maven2/com/netflix/exhibitor/exhibitor-standalone/1.5.5/exhibitor-standalone-1.5.5.jar

ADD include/wrapper.sh /opt/exhibitor/wrapper.sh

USER root
WORKDIR /opt/exhibitor
EXPOSE 2181 2888 3888 8181

ENTRYPOINT ["bash", "-ex", "/opt/exhibitor/wrapper.sh"]
