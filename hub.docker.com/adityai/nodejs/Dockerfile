FROM node
MAINTAINER Aditya Inapurapu adityaii@gmail.com
RUN npm install jimp && npm install text2png && npm install text-to-image && mkdir -p /usr/src/app
EXPOSE 8080
WORKDIR /usr/src/app
ADD . /usr/src/app
