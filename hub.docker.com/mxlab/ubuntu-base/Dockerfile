# Ubuntu 14.04 - Dev base

FROM ubuntu:14.04
MAINTAINER Maxime Lacour <m.lacour@lbp-tm.fr>

RUN apt-get update &&\  
    apt-get install -y software-properties-common curl wget git htop unzip nano &&\
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN useradd dev -m -d /home/dev/ -s /bin/bash

COPY /bin/change-dev-id /usr/local/bin/change-dev-id
RUN chmod +x /usr/local/bin/change-dev-id

