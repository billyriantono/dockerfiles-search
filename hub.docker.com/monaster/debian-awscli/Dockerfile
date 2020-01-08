FROM debian:stretch
EXPOSE 9090

ENV LANG=C.UTF-8

RUN apt-get update && \
  apt-get install -y curl jq && \
  apt-get install -y python-minimal python-pip && \
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install awscli
