FROM jenkins:2.46.1

MAINTAINER  iceihehe "iceihehe@gmail.com"

USER root

RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

RUN apt-get update && apt-get install -y \
        ansible \
        vim
