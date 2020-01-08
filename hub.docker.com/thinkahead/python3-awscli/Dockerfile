FROM alpine:3.7
MAINTAINER Ahead Labs

RUN apk --update --no-cache add \
  python3 \
  jq \
  bash \
  git \
  groff \
  less \
  mailcap \
  bash \
  g++ \
  gcc \
  libxslt-dev 

RUN echo "=> Installing python modules and tidying up" \
  python3 -m ensurepip \
  && rm -r /usr/lib/python*/ensurepip \
  && pip3 install --upgrade pip setuptools \
  && pip3 install --no-cache-dir awscli boto3 datetime \
  && rm -rf /var/cache/apk/* /root/.cache/pip/*

WORKDIR /root
VOLUME /root/.aws

ENTRYPOINT [ "/bin/bash" ]
