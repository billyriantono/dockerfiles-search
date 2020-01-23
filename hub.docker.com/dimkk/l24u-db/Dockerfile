FROM node:latest

MAINTAINER  dimkk


COPY . /var/www
WORKDIR /var/www

RUN npm install

EXPOSE 3000

ENTRYPOINT ["node", "server/server.js"]
