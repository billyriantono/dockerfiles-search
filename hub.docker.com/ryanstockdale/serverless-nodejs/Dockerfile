FROM node:8.12-alpine

RUN apk --no-cache add python python3==3.6.8-r0 python3-dev==3.6.8-r0 py-pip ca-certificates groff less bash make jq curl wget g++   zip git openssh && \
    pip --no-cache-dir install awscli && \
    update-ca-certificates

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget -q https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.25-r0/glibc-2.25-r0.apk && \
    apk add glibc-2.25-r0.apk && \
    rm -f glibc-2.25-r0.apk

RUN npm install -g serverless

ENV SERVERLESS serverless@1.53.0
RUN yarn global add $SERVERLESS
WORKDIR /opt/app

