FROM alpine:latest

# install ansible
RUN apk add --update \
    ansible \
    py-pip \
    && pip3 install \
      boto3 \
      awscli \
    && rm -rf /var/cache/apk/*
