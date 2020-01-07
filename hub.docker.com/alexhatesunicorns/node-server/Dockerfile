FROM node:5

COPY ./src /usr/app/src
COPY ./httpd.js /usr/app
COPY ./package.json /usr/app

RUN \
    apt-get update && \
    apt-get upgrade -y && \
    cd /usr/app && \
    npm install && \
    npm install forever -g



