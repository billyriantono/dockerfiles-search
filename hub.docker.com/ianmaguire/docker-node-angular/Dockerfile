FROM node

MAINTAINER Ian Maguire <mr.scalability@gmail.com>

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
COPY app /usr/src/app
RUN npm install
EXPOSE 8080

CMD node /usr/src/app/server.js
