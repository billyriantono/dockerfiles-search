FROM ubuntu:bionic

WORKDIR /kafka

RUN apt-get update \
    # network utilities
    && apt-get -y install wget curl git \
    # java JRE
    && apt-get install --yes --force-yes openjdk-8-jre \
    # python
    && apt-get install --yes python3 python3-pip

RUN wget https://www-eu.apache.org/dist/kafka/2.4.0/kafka_2.12-2.4.0.tgz && tar -xzf kafka_2.12-2.4.0.tgz

ENTRYPOINT ["/bin/bash"]
