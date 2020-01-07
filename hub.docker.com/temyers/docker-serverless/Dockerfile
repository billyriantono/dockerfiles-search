FROM node:4.3.2

LABEL maintainer=tim.myerscough@magentys.io

RUN npm install -g serverless@1.13.2
RUN npm install serverless-offline --save-dev

VOLUME /project
VOLUME /root/.aws

WORKDIR /project
