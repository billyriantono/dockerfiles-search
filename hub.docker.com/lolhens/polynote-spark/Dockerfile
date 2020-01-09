FROM lolhens/polynote
MAINTAINER LolHens <pierrekisters@gmail.com>


ENV SPARK_VERSION 2.4.4
ENV HADOOP_VERSION 2.7
ENV SPARK_NAME spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}
ENV SPARK_URL https://www-eu.apache.org/dist/spark/spark-${SPARK_VERSION}/${SPARK_NAME}.tgz
ENV SPARK_HOME /opt/$SPARK_NAME
ENV PATH $PATH:$SPARK_HOME/bin


RUN pip3 install \
      pyspark \
 && cleanimage

RUN cd /opt \
 && curl -L $SPARK_URL | tar -xzf -
