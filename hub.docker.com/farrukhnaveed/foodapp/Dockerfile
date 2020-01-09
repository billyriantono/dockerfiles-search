FROM node:latest

MAINTAINER Farrukh Naveed

ENV NODE_ENV=staging

ENV PORT=80

WORKDIR /var/www

COPY package.json .

RUN npm install --quiet

COPY . .

EXPOSE $PORT

RUN npm install nodemon -g

ENTRYPOINT ["nodemon","-L","server.js"]
