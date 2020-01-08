# Version 1.0
FROM phusion/baseimage:latest
MAINTAINER tcloud

USER root

ADD . /tmp/

ENV TERM xterm

RUN sh /tmp/init.sh

VOLUME /data

CMD ["/sbin/my_init"]