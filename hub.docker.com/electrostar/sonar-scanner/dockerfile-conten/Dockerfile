FROM ubuntu:14.04

MAINTAINER 蒼時弦也 "docker@frost.tw"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install git wget -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://cli-assets.heroku.com/branches/stable/heroku-linux-amd64.tar.gz -O heroku.tar.gz && \
    mkdir -p /usr/local/lib && \
    tar -xvzf heroku.tar.gz -C /usr/local/lib && \
    /usr/local/lib/heroku/install && \
    rm heroku.tar.gz

ADD entrypoint.sh /bin/entrypoint

ENTRYPOINT ["/bin/entrypoint"]
