FROM buildpack-deps:xenial-curl

ARG pkg=java-1.8.0-amazon-corretto-jdk_8.212.04-2_amd64.deb
ARG path=https://d3pxv6yz143wms.cloudfront.net/8.212.04.2

RUN apt-get -y update \
    && apt-get -y install java-common \
    && wget $path/$pkg \
    && dpkg --install ./$pkg \
    && rm $pkg \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-amazon-corretto