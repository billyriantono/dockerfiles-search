FROM node:10-alpine

RUN  apk add curl
COPY bin /app/bin/
COPY *.js /app/
COPY *.json /app/
COPY lib /app/lib

RUN  cd /app && npm install -g
