FROM node:10

LABEL MAINTAINER Prolike/drop-gdpr.io

VOLUME /opt/youtransfer/config
VOLUME /opt/youtransfer/uploads

RUN mkdir -p /app
WORKDIR /app

COPY . /app

RUN npm install

EXPOSE 5000

CMD npm run dockerized