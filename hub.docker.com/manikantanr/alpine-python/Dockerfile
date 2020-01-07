FROM alpine:3.5
MAINTAINER Manikantan Ramachandran <manikantanr@biarca.com>
RUN apk add --update libzmq gcc git zeromq-dev yaml-dev python musl-dev make py-pip \
    openssl libffi-dev vim g++ pcre-dev libmagic bash wget curl openssl-dev python-dev && \
    pip install ipython salt requests

ENTRYPOINT bash
