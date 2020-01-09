FROM debian:jessie

LABEL maintainer "https://github.com/amq/"

ENV NODE_VERSION=6.x

RUN apt-get update -y \
    && apt-get install -y curl ruby \
    && curl -sL https://deb.nodesource.com/setup_${NODE_VERSION} | bash - \
    && apt-get install -y nodejs \
    && apt-get clean -y \
    && gem install sass \
    && npm install -g grunt gulp bower

WORKDIR /app
