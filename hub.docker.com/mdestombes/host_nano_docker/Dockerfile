FROM ubuntu:latest

MAINTAINER Matthieu Destombes "matthieu.destombes@activus-services.fr"
LABEL version="1.0"

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y \
    curl \
    iputils-ping \
    nano \
    wget

VOLUME /home/core/dockervolumes/:/tmp/:rw
