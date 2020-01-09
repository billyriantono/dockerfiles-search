FROM ubuntu
MAINTAINER Roy Lines <https://roylines.co.uk>

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get install -y curl

RUN curl http://download.splunk.com/products/splunk/releases/6.3.0/universalforwarder/linux/splunkforwarder-6.3.0-aa7d4b1ccb80-Linux-x86_64.tgz | tar xvz

ENV SPLUNK_HOME /splunkforwarder
ENV PATH $PATH:$SPLUNK_HOME/bin
RUN splunk start --accept-license


