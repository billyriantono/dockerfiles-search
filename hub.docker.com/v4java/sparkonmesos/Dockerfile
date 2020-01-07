FROM  v4java/mesos
MAINTAINER vincent <15091627595@163.com>

ENV MESOS_NATIVE_LIBRARY /usr/local/lib/libmesos.so

ENV SPARK_VERSION 2.1.0-bin-hadoop2.6
RUN apt-get update
RUN apt-get install curl -y
RUN curl -O "https://d3kbcqa49mib13.cloudfront.net/spark-2.2.0-bin-hadoop2.7.tgz" 
RUN tar xf spark-2.2.0-bin-hadoop2.7.tgz
RUN rm spark-2.2.0-bin-hadoop2.7.tgz
RUN mv spark-2.2.0-bin-hadoop2.7 /opt/spark 
RUN apt-get install wget -y

