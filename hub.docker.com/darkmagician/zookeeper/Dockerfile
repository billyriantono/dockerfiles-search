FROM darkmagician/jre:latest

ENV ZK_VER 3.4.8
RUN wget http://apache.opencas.org/zookeeper/zookeeper-${ZK_VER}/zookeeper-${ZK_VER}.tar.gz
RUN tar -xvf zookeeper-${ZK_VER}.tar.gz
RUN rm zookeeper-${ZK_VER}.tar.gz
RUN mv zookeeper-${ZK_VER} /opt/zookeeper/
RUN cp /opt/zookeeper/conf/zoo_sample.cfg /opt/zookeeper/conf/zoo.cfg

EXPOSE 2181
WORKDIR /opt/zookeeper/bin
CMD ["/opt/zookeeper/binzkServer.sh","start-foreground"]



