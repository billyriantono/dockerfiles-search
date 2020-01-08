FROM debian:jessie
MAINTAINER Toshimitsu Takahashi <toshi@tilfin.com>

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        bzip2 \
        libfontconfig \
        curl \
        git \
        build-essential \
        libssl-dev \
        libmysqlclient-dev \
    && apt-get clean \
    && rm -rf /tmp/* /var/lib/apt/lists/*

RUN curl -LO https://nodejs.org/dist/v4.4.7/node-v4.4.7-linux-x64.tar.xz \
    && tar -Jxf node-v4.4.7-linux-x64.tar.xz \
    && cd node-v4.4.7-linux-x64 \
    && cp -R bin include lib share /usr/local

RUN npm install -g gcloud

ENTRYPOINT []
