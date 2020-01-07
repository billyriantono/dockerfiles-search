FROM node:6-alpine

RUN apk add --update --no-cache py-pip ca-certificates jq && \
    pip install awscli --upgrade

RUN apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ add yarn