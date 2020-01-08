FROM amannm/java8-docker-base
MAINTAINER Amann Malik <amannmalik@gmail.com>

ENV HADOOP_VERSION 2.8.1
ENV HADOOP_PREFIX /usr/local/hadoop

RUN wget http://archive.apache.org/dist/hadoop/core/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar --exclude='./share/doc' -zxf /hadoop-${HADOOP_VERSION}.tar.gz && \
    rm /hadoop-${HADOOP_VERSION}.tar.gz && \
    mv hadoop-${HADOOP_VERSION} ${HADOOP_PREFIX}

ENV HIVE_VERSION 2.3.0
ENV HIVE_HOME /usr/local/hive

RUN wget http://archive.apache.org/dist/hive/hive-${HIVE_VERSION}/apache-hive-${HIVE_VERSION}-bin.tar.gz && \
    tar -zxf /apache-hive-${HIVE_VERSION}-bin.tar.gz && \
    rm /apache-hive-${HIVE_VERSION}-bin.tar.gz && \
    mv apache-hive-${HIVE_VERSION}-bin ${HIVE_HOME}