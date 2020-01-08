# Create a distributed Hadoop cluster
#
# Based on taolian/docker-hadoop-env Using Cloudera CDH 5.8
#
# docker build -t taolian/docker-hadoop

FROM taolian/docker-hadoop-env
MAINTAINER Tao Lian<liantao@me.com>

#Remove unused services
#
#Service List:
#
RUN systemctl disable hadoop-hdfs-namenode
RUN systemctl disable hadoop-mapreduce-historyserver
RUN systemctl disable hadoop-yarn-resourcemanager
RUN systemctl disable hbase-regionserver
RUN systemctl disable hadoop-hdfs-datanode  
RUN systemctl disable hadoop-hdfs-secondarynamenode
RUN systemctl disable hadoop-yarn-nodemanager
RUN systemctl disable hbase-master
RUN systemctl disable zookeeper-server

ADD etc/default/bigtop-utils /etc/default/bigtop-utils
ADD etc/default/hadoop-hdfs-namenode /etc/default/hadoop-hdfs-namenode
ADD etc/default/hadoop-hdfs-datanode /etc/default/hadoop-hdfs-datanode
ADD etc/default/hadoop-hdfs-secondarynamenode /etc/default/hadoop-hdfs-secondarynamenode
ADD etc/default/hadoop-0.20-mapreduce /etc/default/hadoop-0.20-mapreduce
ADD etc/default/hadoop-yarn-nodemanager /etc/default/hadoop-yarn-nodemanager
ADD etc/default/hadoop-yarn-resourcemanager /etc/default/hadoop-yarn-resourcemanager
ADD etc/default/hbase /etc/default/hbase
ADD etc/default/hadoop-mapreduce-historyserver /etc/default/hadoop-mapreduce-historyserver

ADD etc/hadoop/conf/core-site.xml /etc/hadoop/conf/core-site.xml
ADD etc/hadoop/conf/hdfs-site.xml /etc/hadoop/conf/hdfs-site.xml