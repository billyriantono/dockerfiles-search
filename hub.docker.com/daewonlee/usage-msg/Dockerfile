FROM node:carbon

MAINTAINER dreamsnail@gmail.com

RUN mkdir -p /usagemsg

WORKDIR /usagemsg

ADD ./ /usagemsg

RUN npm install

ENV NODE_ENV=production

CMD node app.js
