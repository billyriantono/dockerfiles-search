FROM node:8-alpine

RUN apk add --update --no-cache git bash openssh

RUN npm config set unsafe-perm true

RUN npm install hexo-cli -g
RUN npm install gulp-cli -g
RUN npm install firebase-tools -g

EXPOSE 4000
