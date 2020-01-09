FROM ubuntu:utopic

USER root
ENV HOME /root
WORKDIR /root

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en

ADD ./install.sh /tmp/install.sh
RUN /tmp/install.sh
