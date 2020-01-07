FROM ncc0706/alpine-java8:latest

ARG ZOOKEEPER_VERSION=3.4.10
ARG ZK_HOME=/opt/zookeeper-${ZOOKEEPER_VERSION}
ARG ZOOKEEPER_DOWN_MIRROR=http://mirror.tuna.tsinghua.edu.cn

LABEL name="zookeeper" \
      version=${ZOOKEEPER_VERSION} \
      maintainer="niuyuxian <ncc0706@gmail.com>"

RUN apk add --no-cache bash && mkdir /opt \
    && wget -q -O - ${ZOOKEEPER_DOWN_MIRROR}/apache/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz | tar -xzf - -C /opt \
    && mv /opt/zookeeper-${ZOOKEEPER_VERSION}/conf/zoo_sample.cfg /opt/zookeeper-${ZOOKEEPER_VERSION}/conf/zoo.cfg \
    && sed  -i "s|/tmp/zookeeper|$ZK_HOME/data|g" $ZK_HOME/conf/zoo.cfg; mkdir $ZK_HOME/data \
    && rm -rf /tmp

ADD start-zk.sh /usr/local/bin/start-zk.sh

EXPOSE 2181 2888 3888

WORKDIR /opt/zookeeper-${ZOOKEEPER_VERSION}

VOLUME ["/opt/zookeeper-${ZOOKEEPER_VERSION}/conf", "/opt/zookeeper-${ZOOKEEPER_VERSION}/data"]

ENTRYPOINT ["sh","/usr/local/bin/start-zk.sh"]
