FROM node:8.13-alpine
LABEL maintainer="williamf.brtz@gmail.com" version="1.4.0"

RUN apk add --update curl && rm -rf /var/cache/apk/*
RUN npm install --global firebase-tools@latest
