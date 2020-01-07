FROM ubuntu:14.04 
MAINTAINER Justin Liu <xjustinliu@gmail.com>

USER root

#SETTING
ARG SPARK=2.0.0
ARG HADOOP=2.7
ARG JAVA_V=8
ARG JAVA_U=102
ARG JAVA_B=14

#SYSTEM
RUN apt-get update && apt-get install -y curl wget

#SPARK
RUN mkdir /usr/local/spark
RUN curl -s http://d3kbcqa49mib13.cloudfront.net/spark-${SPARK}-bin-hadoop${HADOOP}.tgz | tar -zx -C /usr/local/spark
ENV SPARK_HOME /usr/local/spark/spark-${SPARK}-bin-hadoop${HADOOP}
ENV PATH $PATH:$SPARK_HOME/bin

#JAVA
RUN mkdir /usr/lib/java
RUN wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_V}u${JAVA_U}-b${JAVA_B}/jdk-${JAVA_V}u${JAVA_U}-linux-x64.tar.gz
RUN tar -xf /jdk-${JAVA_V}u${JAVA_U}-linux-x64.tar.gz -C /usr/lib/java
RUN rm /jdk-${JAVA_V}u${JAVA_U}-linux-x64.tar.gz
ENV JAVA_HOME /usr/lib/java/jdk1.${JAVA_V}.0_${JAVA_U}
ENV PATH $PATH:$JAVA_HOME/bin

#MASTER
#RUN mv $SPARK_HOME/conf/slaves.template $SPARK_HOME/conf/slaves
#RUN mv $SPARK_HOME/conf/spark-env.sh.template $SPARK_HOME/conf/spark-env.sh
#RUN echo "export JAVA_HOME=$JAVA_HOME" >> $SPARK_HOME/conf/spark-env.sh
#RUN echo "export SPARK_WORKER_MEMORY=1g" >> $SPARK_HOME/conf/spark-env.sh

#START
CMD ["spark-class", "org.apache.spark.deploy.master.Master"]
