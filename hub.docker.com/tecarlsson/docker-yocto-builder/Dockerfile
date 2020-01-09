# Dockerfile for Ubuntu 14.04 and Oracle Java 8
FROM ubuntu:14.04
MAINTAINER Tobias Karlsson <tecarlsson@gmail.com>

RUN apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install software-properties-common && \
  add-apt-repository ppa:webupd8team/java -y && \
  apt-get update

RUN (echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) && \
  apt-get install -y oracle-java8-installer oracle-java8-set-default
RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
  apt-get -y install \
  build-essential \
  git \
  gawk \
  texinfo \
  chrpath \
  pkg-config \
  libpulse-dev \
  autoconf \
  libsdl1.2-dev \
  libtool \
  lzop \
  corkscrew \
  maven \
  diffstat

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
ENV PATH $JAVA_HOME/bin:$PATH

RUN useradd --create-home --shell /bin/bash builder
USER builder
VOLUME /yocto /home/builder/.m2/repo
ADD start_build.sh /buildscript/start_build.sh
ADD settings.xml /home/builder/.m2/settings.xml

WORKDIR /yocto
ENTRYPOINT ["/buildscript/start_build.sh"]
