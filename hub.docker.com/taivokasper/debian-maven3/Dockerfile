FROM taivokasper/debian-oracle-jdk:latest

MAINTAINER Taivo Käsper <taivo.kasper@gmail.com>

RUN apt-get update -y

WORKDIR /opt

RUN wget --no-check-certificate http://www-eu.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz -O maven.tgz
RUN tar -xzf maven.tgz && rm maven.tgz

ENV M2_HOME /opt/apache-maven-3.3.9
ENV M2 $M2_HOME/bin
ENV MAVEN_OPTS -Xms256m -Xmx512m

WORKDIR /root
ENV PATH ${PATH}:${M2_HOME}/bin

CMD mvn -version
