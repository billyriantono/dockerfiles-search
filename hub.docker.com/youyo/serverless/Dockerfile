FROM node:7-alpine
MAINTAINER youyo

ENV SERVERLESS_VERSION=1.12.1

RUN apk add --no-cache --update ca-certificates openssl curl && \
	npm install -g serverless@${SERVERLESS_VERSION}
