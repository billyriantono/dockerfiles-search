# Tiny generic image to build serverless projects
# Use cases: Bitbucket Pipelines, etc

FROM alpine

RUN apk add --update \
    bash \
    curl \
    git \
    openssh-client \
    nodejs \
    nodejs-npm \
    && rm -rf /var/cache/apk/*

RUN npm install -g \
    serverless \
    babel-cli