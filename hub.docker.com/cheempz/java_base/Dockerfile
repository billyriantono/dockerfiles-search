FROM ubuntu:14.04

SHELL ["/bin/bash", "-c"]

COPY openjdk-ppa.list /etc/apt/sources/list.d/
RUN apt-get update && apt-get install -y software-properties-common \
    && add-apt-repository ppa:openjdk-r/ppa

RUN apt-get update && apt-get install -y \
    apt-transport-https \
    default-jre-headless \
    openjdk-6-jdk \
    openjdk-7-jdk \
    openjdk-8-jdk \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/lib/jvm/java-6-openjdk-amd64/jre/lib/endorsed
COPY jaxws-api-2.2.8.jar .
COPY jaxb-api-2.2.4.jar .

WORKDIR /usr/lib/jvm/java-7-openjdk-amd64/jre/lib/endorsed
COPY jaxws-api-2.2.8.jar .
COPY jaxb-api-2.2.4.jar .

WORKDIR /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/endorsed
COPY jaxws-api-2.2.8.jar .
COPY jaxb-api-2.2.4.jar .

RUN update-alternatives --set java /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java
