FROM ubuntu:latest
MAINTAINER timeloveboy(734991033@qq.com)
RUN apt-get update &&\
    apt-get install -y --fix-missing git-core sudo net-tools iproute2  vim wget curl openssh-server iputils-ping  tree unzip zip &&\
    apt-get clean all
COPY moedocker/xz  /usr/bin/xz 

EXPOSE 22
