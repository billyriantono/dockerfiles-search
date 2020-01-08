#docker built -t sraleik/x64-ubuntu .
FROM ubuntu:trusty
MAINTAINER Sraleik <sraleik@gmail.com>

# Install plugins
ENV TZ=Europe/Paris
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -yq install \
        git \
        vim-tiny && \
    rm -rf /var/lib/apt/lists/* 

