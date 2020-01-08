FROM ubuntu:16.04

MAINTAINER gennady.trafimenkov@gmail.com

RUN apt-get update \
 && apt-get install -y openjdk-8-jre-headless \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
