FROM ubuntu:latest

RUN apt-get update
RUN apt-get install -y software-properties-common python-software-properties debconf-utils apt-transport-https

RUN apt-add-repository -y ppa:webupd8team/java
RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823

RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823
RUN apt-get update
RUN apt-get install -y oracle-java8-installer sbt sbt

RUN mkdir /app
WORKDIR /app