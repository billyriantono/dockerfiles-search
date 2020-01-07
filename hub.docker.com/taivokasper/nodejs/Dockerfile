FROM taivokasper/debian-maven3:latest

MAINTAINER Taivo Käsper <taivo.kasper@gmail.com>

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates

WORKDIR /opt

RUN mkdir nodejs && \
  curl http://nodejs.org/dist/v5.6.0/node-v5.6.0-linux-x64.tar.gz | tar xvzf - -C nodejs --strip-components=1

ENV NODE_HOME /opt/nodejs
ENV PATH $PATH:$NODE_HOME/bin

WORKDIR /root
