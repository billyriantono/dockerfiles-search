FROM alpine:latest

RUN apk --update --no-cache add \
      python \
      py-pip \
      jq \
      bash \
      git \
      groff \
      less \
      mailcap \
      bash \
      && \
    pip install --no-cache-dir awscli && \
    apk del py-pip && \
    rm -rf /var/cache/apk/* /root/.cache/pip/*

WORKDIR /root
VOLUME /root/.aws

ENTRYPOINT [ "aws" ]
