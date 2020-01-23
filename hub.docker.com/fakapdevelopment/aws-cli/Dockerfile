FROM maven:alpine

RUN apk add --no-cache \
    python python-dev py-pip \
    && pip install awscli \
    && pip install --upgrade pip
