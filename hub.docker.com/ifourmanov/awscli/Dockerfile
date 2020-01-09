FROM alpine:3.5
MAINTAINER Ilya Fourmanov <ilya.fourmanov@gmail.com>

RUN apk update && apk add \ 
      bash \
      curl \
      less \
      groff \
      jq \
      python \
      py-pip \
      py2-pip && \
      pip install --upgrade pip awscli s3cmd && \
      mkdir /root/.aws

VOLUME /data
