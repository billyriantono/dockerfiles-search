FROM node:10-alpine

MAINTAINER Daniel Chodusov <daniel@chodusov.com>

RUN mkdir /code
WORKDIR /code
COPY ./index.html /code/index.html
COPY ./package.json /code/package.json
COPY ./package-lock.json /code/package-lock.json
COPY ./index.js /code/index.js
RUN npm install
CMD node index.js
EXPOSE 8081





