FROM ubuntu:16.04

MAINTAINER "Dumitru Cirimpei" <cirimpei.dumitru@gmail.com>

RUN mkdir -p /var/www \
    && echo '{ "allow_root": true }' > /root/.bowerrc \
    && apt-get update \
    && apt-get install -y curl git \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs \
    && apt-get install -y build-essential \
    && npm install -g bower gulp gulp-cli jshint nodemon npm-check-updates \
    && curl "https://install.meteor.com/?release=1.6.1" | sh

#FROM node:8.11
#RUN chown node: /root

#USER node
#RUN curl "https://install.meteor.com/?release=1.6.1" | sh
#ENV PATH="/home/node/.meteor:${PATH}"

VOLUME /var/www
VOLUME /var/www/node_modules

EXPOSE 3000
