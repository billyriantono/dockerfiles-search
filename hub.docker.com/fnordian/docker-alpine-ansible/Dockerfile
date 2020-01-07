FROM alpine:3.8

MAINTAINER Marcus Hunger <marcus.hunger@gmail.com>

RUN apk add --no-cache openssh curl python3 py-cffi py3-bcrypt py3-cryptography py3-pynacl && \
    pip3 install boto3 awscli ansible==2.7.10 && \
    rm -rf /tmp/*
