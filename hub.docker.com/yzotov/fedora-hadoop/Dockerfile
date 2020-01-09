FROM yzotov/fedora-common:23.1

MAINTAINER Yuriy Zotov <yura.zotov@gmail.com>

RUN curl -Lk http://www.eu.apache.org/dist/hadoop/common/hadoop-2.7.2/hadoop-2.7.2.tar.gz | tar -xz -C /opt
RUN ln -s /opt/hadoop-2.7.2 /opt/hadoop

ENV HADOOP_HOME /opt/hadoop
ENV HADOOP_PREFIX /opt/hadoop
