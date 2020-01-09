FROM anapsix/alpine-java
LABEL Daniele Vitale "vitaled@gmail.com"

ARG SPARK_VERSION=2.3.1
ARG HADOOP_VERSION=2.7
ARG SPARK_PACKAGE=spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}
RUN apk add --update curl bash wget

RUN wget -q http://www-eu.apache.org/dist/spark/spark-${SPARK_VERSION}/${SPARK_PACKAGE}.tgz
RUN tar -xzf ${SPARK_PACKAGE}.tgz -C /usr/local
RUN ln -s /usr/local/${SPARK_PACKAGE} /usr/local/spark
ENV SPARK_HOME=/usr/local/spark
ENV PATH=$PATH:${SPARK_HOME}/bin
