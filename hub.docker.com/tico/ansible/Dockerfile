FROM python:alpine

ARG deps="alpine-sdk build-base openssl-dev libffi-dev python3-dev"

RUN apk --no-cache add openssh-client $deps && \
    pip install ansible boto boto3 && \
    apk --no-cache del $deps
