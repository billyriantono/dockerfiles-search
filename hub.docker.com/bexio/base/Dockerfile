FROM ubuntu:trusty

USER root
ENV HOME /root
WORKDIR /root

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en

ADD ./install-base.sh /tmp/install-base.sh
RUN /tmp/install-base.sh
