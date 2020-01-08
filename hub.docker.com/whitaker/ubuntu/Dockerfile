FROM ubuntu:16.04
MAINTAINER Jason Whitaker <jason@thewhitakers.ca>

RUN apt-get update && \
    apt-get install -y net-tools iputils-ping curl software-properties-common && \
    rm -rf /var/lib/apt/lists/*
