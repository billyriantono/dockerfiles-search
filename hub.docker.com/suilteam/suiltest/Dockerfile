FROM node:alpine
MAINTAINER "Carter Mbotho <carter@suilteam.com>"

RUN npm install -g mocha mocha-junit-reporter
RUN adduser -s /bin/sh -h /home/suiltest -D suiltest
WORKDIR /home/suiltest

RUN npm install --save-dev chai && \
    npm install --save-dev chai-http && npm install
