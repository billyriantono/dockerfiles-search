FROM node:8-alpine as builder

RUN apk update && apk --update add --virtual build-dependencies build-base git python2

WORKDIR /app 

RUN  npm install -g webpack-cli -D
RUN  npm install -g @angular/cli -v 1.6.8 -D
RUN  npm install -g bugsnag-sourcemaps
RUN  npm install -g rename-cli


