FROM java:8

MAINTAINER Toni Pohl <info@toni-pohl.de>

ENV SPARK_VERSION=2.1.1
ENV HADOOP_VERSION=2.7
ENV PATH=$PATH:/spark/bin:/spark/sbin

RUN apt-get update && apt-get install -y python3 python3-setuptools python3-pip

ADD http://d3kbcqa49mib13.cloudfront.net/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz .
RUN tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

RUN chmod +x /spark/bin/load-spark-env.sh && chmod +x /spark/sbin/spark-config.sh
