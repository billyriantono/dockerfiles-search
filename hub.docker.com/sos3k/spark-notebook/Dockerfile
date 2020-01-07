FROM bde2020/hadoop-base
MAINTAINER Radoslaw Wojciechowski <radoslaw.wojciechowski@gmail.com>

ENV SPARK_NOTEBOOK_VERSION 0.7.0
ENV SCALA_VERSION 2.11.8
ENV SPARK_VERSION 2.0.1
ENV HADOOP_VERSION 2.7.2

RUN set -x \
    && curl -fSL "https://www.dropbox.com/s/t4qbf7ayy679bmc/spark-notebook-$SPARK_NOTEBOOK_VERSION-scala-$SCALA_VERSION-spark-$SPARK_VERSION-hadoop-$HADOOP_VERSION-with-hive-with-parquet.tar" -o /tmp/spark-notebook.tgz \
    && tar -xzvf /tmp/spark-notebook.tgz -C /opt/ \
    && mv /opt/spark-notebook-* /opt/spark-notebook \
    && rm /tmp/spark-notebook.tgz

COPY run.sh /run.sh
RUN chmod a+x /run.sh

WORKDIR /opt/spark-notebook/

CMD ["/run.sh"]
