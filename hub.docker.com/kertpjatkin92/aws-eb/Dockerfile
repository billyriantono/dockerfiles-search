FROM alpine:3.10.1
MAINTAINER Kert Pjatkin <kertpjatkin@gmail.com>

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
    nodejs \
    nodejs-npm \
    yarn \
    && pip install --no-cache-dir awscli \
    && pip install --no-cache-dir boto3 \
    && apk del py-pip \
    && rm -rf /var/cache/apk/* /root/.cache/pip/*

WORKDIR /root
VOLUME /root/.aws

RUN apk update
RUN apk add linux-headers
RUN apk add --no-cache git bash build-base libffi-dev openssl-dev bzip2-dev zlib-dev readline-dev sqlite-dev
RUN apk add --no-cache curl openssh-client

ENV NODE_VERSION 10.16.0

RUN git clone https://github.com/aws/aws-elastic-beanstalk-cli-setup.git
RUN ./aws-elastic-beanstalk-cli-setup/scripts/bundled_installer
ENV PATH "$PATH:/root/.ebcli-virtual-env/executables"
