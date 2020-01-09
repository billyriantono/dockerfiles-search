FROM node:latest
LABEL maintainer="KPTAC Technologies"

RUN set -xe \
    && apt-get update \
    && apt-get -yq install bash git openssh-server \
    && npm install -g npm \
    && apt-get -yq clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && git --version && bash --version && ssh -V && npm -v && node -v && yarn -v

RUN npm install -g expo-cli