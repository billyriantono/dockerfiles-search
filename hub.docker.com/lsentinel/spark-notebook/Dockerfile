FROM lsentinel/hadoop-base

ENV APACHE_SPARK_VERSION 1.6.0
ENV APACHE_HADOOP_VERSION 2.7.1
ENV SPARK_NOTEBOOK_VERSION 0.6.2
ENV SCALA_VERSION 2.11.7

RUN set -x \
    && curl -fSL "https://s3.eu-central-1.amazonaws.com/spark-notebook/tgz/spark-notebook-$SPARK_NOTEBOOK_VERSION-scala-$SCALA_VERSION-spark-$APACHE_SPARK_VERSION-hadoop-$APACHE_HADOOP_VERSION.tgz?max-keys=100000" -o /tmp/spark-notebook.tgz \
    && tar -xzvf /tmp/spark-notebook.tgz -C /opt/ \
    && mv /opt/spark-notebook-* /opt/spark-notebook \
    && rm /tmp/spark-notebook.tgz

COPY run.sh /run.sh
RUN chmod a+x /run.sh

WORKDIR /opt/spark-notebook/

CMD ["/run.sh"]