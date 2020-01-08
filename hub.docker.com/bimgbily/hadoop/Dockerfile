FROM bimgbily/centos-java:latest

RUN wget http://apache-mirror.rbc.ru/pub/apache/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz
RUN mkdir -p /opt/lib \
      && tar -xvf hadoop-3.2.1.tar.gz -C /opt/lib \
      && rm -rf hadoop-3.2.1.tar.gz

ENV PATH=${PATH}:/opt/lib/hadoop-3.2.1/bin
ENV HADOOP_CONF_DIR=/etc/hadoop