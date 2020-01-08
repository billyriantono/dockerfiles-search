# Dockerfile for rawevan/ubuntu:basetools
FROM ubuntu:16.04
MAINTAINER Evan <liaiwen_mail@163.com>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget && \
    # change sources.list
    wget -O sources.list https://raw.githubusercontent.com/RawEvan/dockerfiles/ubuntu/evan/ubuntu/sources.list && \
    #mv sources.list /etc/apt/sources.list && \
    # update apt-get
    apt-get update && \
    apt-get upgrade -y && \
    # install curl
    apt-get install -y curl

ENV HOME /root
WORKDIR $HOME
