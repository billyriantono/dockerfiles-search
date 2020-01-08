FROM superuserltd/centos-7-java-8-openjdk-headle

MAINTAINER ramon.gordillo@super-user.net

ENV ZOOKEEPER_VERSION=3.4.6
ENV INSTALL_HOME=/opt
ENV ZK_HOME=${INSTALL_HOME}/zookeeper-${ZOOKEEPER_VERSION}

# Also you can do it with ADD http://apache.rediris.es/zookeeper/stable/zookeeper-${ZOOKEEPER_VERSION}.tar.gz /opt

RUN yum -y install tar
RUN curl -L https://archive.apache.org/dist/zookeeper/zookeeper-${ZOOKEEPER_VERSION}/zookeeper-${ZOOKEEPER_VERSION}.tar.gz | tar -xzf - -C ${INSTALL_HOME}

COPY zoo-${ZOOKEEPER_VERSION}.cfg ${ZK_HOME}/conf/zoo.cfg

RUN mkdir ${ZK_HOME}/data
RUN sed  -i "s|/tmp/zookeeper|${ZK_HOME}/data|g" ${ZK_HOME}/conf/zoo.cfg

# In case distributed is needed: 
#EXPOSE 2181 2888 3888
EXPOSE 2181
WORKDIR ${ZK_HOME}
VOLUME ["${ZK_HOME}/conf", "${ZK_HOME}/data"]

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:${ZK_HOME}/bin

CMD ["zkServer.sh", "start-foreground"]
