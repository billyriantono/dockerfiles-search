FROM node:boron
MAINTAINER Björn Wenzel <bjoern.wenzel@tomm-apps.de>

ENV IONIC_VERSION 2.2.1

RUN npm install -g gulp bower ionic@${IONIC_VERSION} cordova
RUN mkdir data
RUN adduser user
USER user
