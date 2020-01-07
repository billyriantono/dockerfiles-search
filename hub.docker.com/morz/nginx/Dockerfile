FROM ubuntu:trusty

MAINTAINER Mohd Rozi <blackrosezy@gmail.com>

# Install packages
RUN echo "deb http://ppa.launchpad.net/nginx/stable/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/nginx-stable-$(lsb_release -cs).list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C300EE8C

RUN DEBIAN_FRONTEND=noninteractive; apt-get update && apt-get -y \
    install python-pip nginx dos2unix wget curl \
    && rm -rf /var/lib/apt/lists/*

RUN pip install supervisor dumb-init
RUN mkdir -p /var/log/supervisor