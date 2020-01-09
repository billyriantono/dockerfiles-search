FROM ubuntu:18.10
LABEL maintainer "Sharedcloud <admin@sharedcloud.io>"

RUN \
  apt-get update && \
  apt-get install -y nodejs

RUN mkdir -p /data

WORKDIR /data

CMD /bin/bash && nodejs -e "$CODE"
