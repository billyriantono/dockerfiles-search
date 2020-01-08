FROM gtrafimenkov/ubuntu1604-openjdk-8-jdk

MAINTAINER gennady.trafimenkov@gmail.com

RUN apt-get update \
 && apt-get install -y apt-transport-https \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

COPY sbt.list /etc/apt/sources.list.d

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823 \
  && apt-get update \
  && apt-get -y install sbt \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
