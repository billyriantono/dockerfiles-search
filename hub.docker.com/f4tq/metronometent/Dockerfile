#Build spark-1.3.0 master-image on Ubuntu 14.04.1

FROM ubuntu:14.04.1
MAINTAINER Izhar ul Hassan "ezhaar@gmail.com"

USER root

RUN apt-get update && apt-get install -y \
  wget \ 
  openjdk-7-jdk \
  supervisor \
  openssh-server

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

# Setup a tmp volume for downloads
VOLUME ["/tmp"]

# SCALA
RUN /usr/bin/wget \
  http://scala-lang.org/files/archive/scala-2.10.4.tgz \
  -P /tmp && tar -xzf /tmp/scala-2.10.4.tgz -C /usr/local/ && rm -rf /tmp/*

RUN ln -s /usr/local/scala-2.10.4 /usr/local/scala
ENV PATH $PATH:/usr/local/scala/bin

COPY spark_conf/ssh_config /etc/ssh/

# SPARK
ENV SPARK_HOME /usr/local/spark
ENV SPARK_CONF_DIR /usr/local/spark/conf

RUN /usr/bin/wget \
  http://d3kbcqa49mib13.cloudfront.net/spark-1.3.0-bin-hadoop2.4.tgz \
  -P /tmp && tar -xzf /tmp/spark-1.3.0-bin-hadoop2.4.tgz -C /usr/local/ && rm -rf /tmp/*

RUN mv /usr/local/spark-1.3.0-bin-hadoop2.4 /usr/local/spark
RUN mv $SPARK_CONF_DIR/log4j.properties.template $SPARK_CONF_DIR/log4j.properties

ENV PATH $PATH:/usr/local/spark/bin:/usr/local/spark/sbin
COPY spark_conf/spark-env.sh $SPARK_CONF_DIR/
ENV TERM xterm

RUN mkdir -p /var/run/sshd /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN ssh-keygen -q -t rsa -P '' -f /root/.ssh/id_rsa 
ENV TERM xterm
CMD ["/usr/bin/supervisord"]
