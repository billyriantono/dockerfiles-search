FROM consol/ubuntu-xfce-vnc:latest

MAINTAINER Gaston Maron "gastonmaron@gmail.com"
ENV REFRESHED_AT 2017-08-30

USER 0

RUN apt-get update && apt-get -y upgrade \
    && apt-get install -y build-essential \
    && apt-get install -y nano \
    && apt-get install -y net-tools \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:openjdk-r/ppa \
    && apt-get update \
    && apt-get install -y openjdk-7-jdk \
    && apt-get install -y rpcbind 
    
USER 1984

