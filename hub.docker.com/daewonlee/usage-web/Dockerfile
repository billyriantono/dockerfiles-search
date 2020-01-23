FROM node:carbon

MAINTAINER dreamsnail@gmail.com

RUN mkdir -p /usageweb

WORKDIR /usageweb

ADD ./ /usageweb

RUN npm install

ENV NODE_ENV=production

CMD node app.js
