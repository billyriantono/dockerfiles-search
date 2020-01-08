FROM ubuntu:latest

RUN apt-get update

RUN apt-get install --yes vim
RUN apt-get install --yes curl
RUN apt-get install --yes nodejs
RUN apt-get install --yes nodejs-legacy
RUN apt-get install --yes npm

COPY . /usr/src/nodeapp

#cd into nodeapp
WORKDIR /usr/src/nodeapp

RUN node server.js

CMD ["node","server.js"]

