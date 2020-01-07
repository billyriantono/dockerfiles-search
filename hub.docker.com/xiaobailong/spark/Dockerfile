FROM xiaobailong/oracle-java:java8

ENV YARN_CONF_DIR "/data/yarn-conf"
ENV HADOOP_USER_NAME "hdfs"
ENV SPARK_HOME "/data/spark-2.0.1-bin-hadoop2.6/"

# install spark
RUN cd /data && \
    wget -qc "http://shinyfeather.com/spark/spark-2.0.1/spark-2.0.1-bin-hadoop2.6.tgz" && \
    tar -xf spark-2.0.1-bin-hadoop2.6.tgz && \
    rm -rf spark-2.0.1-bin-hadoop2.6.tgz && \
    ln -s "/data/spark-2.0.1-bin-hadoop2.6/bin/"* "/usr/bin/"
