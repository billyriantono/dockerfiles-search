FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    nodejs \
    npm \
    vim

RUN npm install -g @beaker/homebase
RUN npm i -g pm2

VOLUME /config

CMD homebase --config /config/main.yml
