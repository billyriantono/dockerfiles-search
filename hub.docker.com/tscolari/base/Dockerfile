# RUBY MACHINE
FROM stackbrew/ubuntu
MAINTAINER Tiago Scolari <tscolari@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get upgrade -y --force-yes &&\
    apt-get install -y --force-yes \
                         vim && \
    apt-get clean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./vimrc /etc/vim/vimrc
