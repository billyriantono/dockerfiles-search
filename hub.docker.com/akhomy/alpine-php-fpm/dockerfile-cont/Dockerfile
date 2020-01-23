FROM java:openjdk-8

RUN mkdir /opt/spark
WORKDIR /opt/spark
ADD http://d3kbcqa49mib13.cloudfront.net/spark-1.4.0-bin-hadoop2.6.tgz /tmp/

RUN tar -zxf /tmp/spark-1.4.0-bin-hadoop2.6.tgz -C /opt/spark --strip-components=1
RUN apt-get update
RUN apt-get install -y build-essential python-dev python-boto libcurl4-nss-dev libsasl2-dev maven libapr1-dev libsvn-dev zlib1g-dev

RUN update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

RUN wget http://www.apache.org/dist/mesos/0.22.1/mesos-0.22.1.tar.gz
RUN tar -zxf mesos-0.22.1.tar.gz
RUN cd mesos-0.22.1 && ./configure && make

RUN wget http://supergsego.com/apache/hadoop/common/hadoop-2.6.0/hadoop-2.6.0.tar.gz
RUN tar -zxf hadoop-2.6.0.tar.gz

ENV MESOS_NATIVE_LIBRARY /opt/spark/mesos-0.22.1/src/.libs/libmesos.so
ENV HADOOP_HOME /opt/spark/hadoop-2.6.0
