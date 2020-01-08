FROM ubuntu:latest
LABEL maintainer "Best Sira <sirawat21@gmail.com>"
RUN apt-get update -y
RUN apt-get install -y git npm nodejs
RUN npm update
RUN npm install -g nodemon
RUN npm install
WORKDIR /www
