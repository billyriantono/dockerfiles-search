## -*- docker-image-name: "everpeace/hbase-standalone" -*-
FROM ubuntu:14.04
MAINTAINER Shingo Omura everpeace@gmail.com

ENV DEBIAN_FRONTEND noninteractive

# install add-apt-repository
RUN \
  apt-get update && \
  apt-get install -y software-properties-common curl

# install java
RUN \
  echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer

# install hbase master
RUN mkdir /opt/hbase
RUN wget http://archive.cloudera.com/cdh5/cdh/5/hbase-1.2.0-cdh5.7.1.tar.gz -O /opt/hbase/hbase-1.2.0-cdh5.7.1.tar.gz
RUN cd /opt/hbase && tar xfvz hbase-1.2.0-cdh5.7.1.tar.gz
ADD hbase-site.xml /etc/hbase/conf/hbase-site.xml

# need this for hbase to run
ENV JAVA_HOME /usr

# zookeeper
EXPOSE 2181
# HBase Master API port
EXPOSE 60000
# HBase Master Web UI
EXPOSE 60010
# Regionserver API port
EXPOSE 60020
# HBase Regionserver web UI
EXPOSE 60030

CMD /opt/hbase/hbase-1.2.0-cdh5.7.1/bin/hbase master start
