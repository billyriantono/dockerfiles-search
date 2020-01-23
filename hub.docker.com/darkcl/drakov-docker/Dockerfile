FROM node:alpine
MAINTAINER Yeung Yiu Hung <hkclex@gmail.com>

RUN mkdir -p /app/
WORKDIR /app

COPY . .

RUN npm install -g drakov
EXPOSE 3000
CMD drakov --config ./config.js -p 3000 --public