FROM niro/java

MAINTAINER Nirosan <pnirosan@gmail.com>

ENV SPARK_VERSION 1.6.0
ENV HADOOP_VERSION 2.6

RUN curl -s http://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz | tar -xz -C /usr/local/
RUN cd /usr/local && ln -s spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION spark
ENV SPARK_HOME /usr/local/spark
