FROM centos:7
MAINTAINER Motasem Salem <motasem@gmail.com>

ENV JAVA_HOME /usr/java/jdk1.8.0_65

RUN curl -OL -b "oraclelicense=a" http://download.oracle.com/otn-pub/java/jdk/8u65-b17/jdk-8u65-linux-x64.rpm

RUN yum install -y jdk-8u65-linux-x64.rpm

RUN curl -OL http://apachemirror.ovidiudan.com/spark/spark-1.5.2/spark-1.5.2-bin-hadoop2.6.tgz
RUN tar xvf spark-1.5.2-bin-hadoop2.6.tgz -C /usr/local
RUN rm -f spark-1.5.2-bin-hadoop2.6.tgz jdk-8u65-linux-x64.rpm

COPY entry-point.sh /entry-point.sh

#RUN /usr/local/spark-1.5.2-bin-hadoop2.6/sbin/start-master.sh

EXPOSE 8080 7077 4040

ENTRYPOINT ["/entry-point.sh"]
#CMD tail -f /usr/local/spark-1.5.2-bin-hadoop2.6/logs/*.out
