FROM stfnltnr/hadoop:3.2.0
# spark version
ARG SPARK_VERSION=2.4.1
# download and install spark
RUN \
  wget http://mirror.klaus-uwe.me/apache/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop2.7.tgz && \
  tar -xzf spark-$SPARK_VERSION-bin-hadoop2.7.tgz && \
  mv spark-$SPARK_VERSION-bin-hadoop2.7 $HADOOP_HOME/spark
# set environment vars for Spark
ENV SPARK_HOME $HADOOP_HOME/spark
ENV LD_LIBRARY_PATH=$HADOOP_HOME/lib/native:$LD_LIBRARY_PATH
# create directory spark-events
RUN mkdir /tmp/spark-events
# remove downloaded files
RUN rm -rf /spark-$SPARK_VERSION-bin-hadoop2.7.tgz 
# Spark ports
EXPOSE 4040 18080
