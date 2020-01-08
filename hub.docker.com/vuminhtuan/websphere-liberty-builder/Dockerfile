FROM websphere-liberty:18.0.0.4-webProfile7
USER root
MAINTAINER Minh Tuan Vu <me@minhtuanvu.com>

ENV ANT_VERSION 1.9.14

RUN \
  apt-get update && \
  # install utilities
  apt-get install -y \
    wget \
    curl \
    vim \
    git \
    zip \
    bzip2 \
    openjdk-8-jdk && \
  # cleanup
  apt-get clean && \
  rm -rf \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/*

RUN cd && \
    wget -q https://www-us.apache.org/dist//ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
    mv apache-ant-${ANT_VERSION} /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz

ENV ANT_HOME /opt/ant
ENV PATH ${PATH}:/opt/ant/bin

ENV WLP_HOME=/opt/ibm/wlp
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

USER 1001
