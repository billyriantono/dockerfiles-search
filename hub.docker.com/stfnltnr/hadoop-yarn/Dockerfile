FROM ubuntu:18.04

ARG HADOOP_VERSION=3.1.2
ARG SPARK_VERSION=2.3.3

# install packages
RUN \
  apt-get update && apt-get install -y \
  ssh \
  rsync \
  vim \
  openjdk-8-jdk-headless

# SSH
RUN mkdir -p /root/.ssh
ADD id_rsa.pub /root/.ssh/id_rsa.pub
ADD id_rsa.pub /root/.ssh/authorized_keys
ADD ssh_config /root/.ssh/config
RUN chmod 600 /root/.ssh/config && chown root:root /root/.ssh/config

# set environment vars
ENV HADOOP_HOME /opt/hadoop
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV HADOOP_COMMON_HOME /opt/hadoop
ENV HADOOP_HDFS_HOME /opt/hadoop
ENV HADOOP_MAPRED_HOME /opt/hadoop
ENV HADOOP_YARN_HOME /opt/hadoop
ENV HADOOP_CONF_DIR /opt/hadoop/etc/hadoop
ENV YARN_CONF_DIR $HADOOP_HOME/etc/hadoop

# download and extract hadoop, set JAVA_HOME in hadoop-env.sh
RUN \
  wget http://apache.mirrors.tds.net/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz && \
  tar -xzf hadoop-$HADOOP_VERSION.tar.gz && \
  mv hadoop-$HADOOP_VERSION $HADOOP_HOME && \
  echo "export JAVA_HOME=$JAVA_HOME" >> $HADOOP_HOME/etc/hadoop/hadoop-env.sh

# copy hadoop configs
# ADD *xml $HADOOP_HOME/etc/hadoop/

# create data
VOLUME /hdfs/volume1

# install spark
RUN \
  wget http://mirror.klaus-uwe.me/apache/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop2.7.tgz && \
  tar -xzf spark-$SPARK_VERSION-bin-hadoop2.7.tgz && \
  mv spark-$SPARK_VERSION-bin-hadoop2.7 $HADOOP_HOME/spark

# set environment vars for Spark
ENV SPARK_HOME $HADOOP_HOME/spark
ENV LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH

# copy spark config file
# ADD spark-defaults.conf $SPARK_HOME/conf/

# create directory spark-events
RUN mkdir /tmp/spark-events

# update path
RUN echo PATH=$PATH:$JAVA_HOME/bin:$HADOOP_HOME/bin:$SPARK_HOME/bin >> ~/.bashrc 

# expose various ports
EXPOSE 8030 8031 8032 8033 8088 10020 19888 22 4040 18080

# remove downloaded files
RUN rm -rf /spark-$SPARK_VERSION-bin-hadoop2.7.tgz /hadoop-$HADOOP_VERSION.tar.gz

# copy script to start yarn and spark history server
ADD start-yarn.sh start-yarn.sh

# start yarn and spark history server
CMD bash start-yarn.sh