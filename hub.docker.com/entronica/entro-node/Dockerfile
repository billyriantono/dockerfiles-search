# Use an official Node runtime as the parent image
FROM node:8.12-alpine
ARG TZ=Asia/Bangkok

#if you are using an alpine based image you have to install the tzdata first. 
RUN apk add --no-cache tzdata

RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} > /etc/timezone
RUN npm i pm2 -g 
