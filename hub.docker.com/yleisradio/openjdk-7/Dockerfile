FROM ubuntu:trusty

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
            openjdk-7-jdk && \
    rm -rf /var/lib/apt/lists/*
