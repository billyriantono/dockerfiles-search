FROM python:2.7-alpine

MAINTAINER Timoteo Ponce <timo.slack@gmail.com>

RUN apk add --update alpine-sdk \
  && apk add --update build-base libffi-dev \
  && apk add --update openssl openssl-dev \
  && pip install cffi && pip install fabric 
