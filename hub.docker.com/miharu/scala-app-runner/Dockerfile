FROM ubuntu:18.04

MAINTAINER Toshiaki Inahata <inahata@miharu.co.jp>


RUN set -x \
        && apt-get update \
        && apt-get upgrade -y \
        && apt-get install -y openjdk-8-jre openjdk-8-jdk \
        \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*
