FROM ubuntu:18.04

MAINTAINER alex

RUN apt-get update && \
apt-get upgrade -y && \
apt-get install -y telnet && \
apt-get install -y software-properties-common && \
add-apt-repository ppa:webupd8team/java -y && \
apt-get update && \
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
apt-get install -y oracle-java8-installer && \
apt-get clean && \
apt-get autoremove -y && \
apt-get autoclean

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV PATH "$PATH":${JAVA_HOME}/bin:.:
