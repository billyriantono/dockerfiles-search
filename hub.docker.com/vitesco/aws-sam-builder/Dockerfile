FROM python:3.7-alpine

RUN apk add --no-cache \
      bash \
      jq \
      perl

RUN apk add --no-cache --virtual .build-deps  \
      gcc \
      libc-dev && \
    pip install --upgrade pip && \
    pip install --no-cache-dir \
      awscli \
      aws-sam-cli \
      pytest \
      pytest-mock \
      boto3 \
      six==1.11.0 && \
    apk del --no-cache .build-deps

ENTRYPOINT [ "/bin/sh" ]
