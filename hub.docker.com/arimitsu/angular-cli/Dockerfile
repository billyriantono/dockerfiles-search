FROM node:8.11.1
MAINTAINER Y.Arimitsu<arimitu@ouk.jp>

RUN dpkg --add-architecture i386 && apt-get update && apt-get install build-essential -y

ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
ENV PATH=$PATH:/home/node/.npm-global/bin
USER node

RUN npm install -g @angular/cli@1.7.4

EXPOSE 4200
EXPOSE 49153

WORKDIR /home/node/app
VOLUME /home/node/app

