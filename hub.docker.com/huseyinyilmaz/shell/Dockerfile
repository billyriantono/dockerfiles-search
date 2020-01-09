FROM ubuntu:latest

MAINTAINER Huseyin Yilmaz <yilmazhuseyin@gmail.com>

RUN apt-get update && \
    apt-get install -y ssh \
                       iputils-ping \
                       wget \
                       curl \
                       git \
                       zip \
                       make \
                       emacs \
                       dnsutils \
                       nmap && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
