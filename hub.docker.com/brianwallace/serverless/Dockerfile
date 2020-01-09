# inherit from golang
FROM node:9.2-alpine

MAINTAINER Brian Wallace <bpwallace@gmail.com>

# Used for forcing update of deps
ENV BUILDDATE 20171120
ENV SERVERLESS_VERSION=1.24.1


RUN apk --no-cache update && \
    apk --no-cache add mysql-client python py-pip py-setuptools ca-certificates curl groff less && \
    pip --no-cache-dir install awscli && \
    rm -rf /var/cache/apk/*

RUN npm install -g serverless@${SERVERLESS_VERSION}

RUN serverless
RUN serverless --version
