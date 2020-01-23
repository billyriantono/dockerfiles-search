FROM openjdk:8u151-jdk
LABEL name=seren-jdk
LABEL version=0.2

RUN apt-get update \
    && cat /etc/apt/sources.list \
    && apt-get install -y openjdk-8-dbg \
    && apt-get autoclean \
    && apt-get clean \
    && apt-get autoremove
