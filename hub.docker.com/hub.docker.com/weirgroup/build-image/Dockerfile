# This dockerfile builds the zap stable release
# Additional support for nodejs, cypress, @slack/client, retire.js and wait-on.

FROM owasp/zap2docker-stable:latest
LABEL maintainer=""

USER root
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 8.16.0
ENV ZAP_PORT 8090

RUN apt-get update \
    && apt-get upgrade -y \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs xvfb libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 zip \
    && npm install -g react-tools @slack/client wait-on retire \
    && npm install cypress \
    && pip install --upgrade pip git+https://github.com/Grunny/zap-cli.git \
    && npm install -g npm@latest
    
EXPOSE 8090
