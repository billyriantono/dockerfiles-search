FROM yzotov/fedora-common:23.1

MAINTAINER Yuriy Zotov <yura.zotov@gmail.com>

RUN curl -Lk http://www.eu.apache.org/dist/spark/spark-1.6.1/spark-1.6.1-bin-hadoop2.6.tgz | tar -xz -C /opt
RUN ln -s /opt/spark-1.6.1-bin-hadoop2.6 /opt/spark

ENV SPARK_HOME /opt/spark
ENV SPARK_PREFIX /opt/spark

