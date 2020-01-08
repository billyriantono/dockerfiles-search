FROM ubuntu
RUN apt-get update &&\
    DEBIAN_FRONTEND=noninteractive apt-get install -y wget xz-utils git &&\
    rm -rf /var/lib/apt/lists/*

ENV NODE_VERSION=v13.2.0

WORKDIR /root
VOLUME /root

RUN wget https://nodejs.org/dist/$NODE_VERSION/node-$NODE_VERSION-linux-x64.tar.xz &&\
    tar xJf node-$NODE_VERSION-linux-x64.tar.xz && cd node-$NODE_VERSION-linux-x64 && cp -ra * /usr/local &&\
    cd /root && rm -rf node-$NODE_VERSION-linux-x64*
