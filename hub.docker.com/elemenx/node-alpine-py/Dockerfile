FROM node:12-alpine

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    ca-certificates \
    openssl && \
    update-ca-certificates && \
    pip install --upgrade pip
