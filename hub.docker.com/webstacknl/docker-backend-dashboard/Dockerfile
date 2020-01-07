FROM node:12-alpine
MAINTAINER Robbert van Mourik, robbert@webstack.nl

RUN apk update
RUN apk add docker openrc
RUN rc-update add docker boot

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 9090
CMD [ "node", "server.js" ]