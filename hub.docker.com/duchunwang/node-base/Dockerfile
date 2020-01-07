FROM node:alpine

LABEL version="1.0"

ADD package.json /usr/src/
WORKDIR /usr/src/

RUN npm install

ONBUILD ADD server.js /usr/src/

ENTRYPOINT node server.js

EXPOSE 80 