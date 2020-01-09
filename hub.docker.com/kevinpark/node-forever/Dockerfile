FROM node:8.11.3
MAINTAINER Woong-Gi Jeon<jeon.wbbi@gmail.com>

RUN mkdir -p /var/node/app/src

ADD ./app/ /var/node/app/

WORKDIR /var/node/app

RUN npm install mysql

RUN npm install socket.io

RUN npm install express

RUN npm install forever -g

RUN npm install redis

RUN npm install html-entities

CMD forever /var/node/app/src/server.js