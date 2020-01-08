FROM node:10-alpine
MAINTAINER rh389
RUN apk update 
RUN apk -U add yarn git openssh docker curl python make g++
RUN mkdir ~/workspace && chmod -R 777 ~/workspace
