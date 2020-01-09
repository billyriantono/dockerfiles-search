FROM ubuntu:16.04

RUN apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get -y install texlive-full

RUN mkdir /data
WORKDIR /data
CMD /bin/bash 
