FROM php:7.2-alpine

RUN apk add --update \
  bash \
  build-base \
  ca-certificates \
  curl \
  gcc \
  git \
  jq \
  libc6-compat \
  libffi-dev \
  libffi-dev \
  libxml2-dev \
  libxslt-dev \
  make \
  musl-dev \
  openssl \
  openssl-dev \
  py-pip \
  python2-dev \
  composer \
  yarn

RUN pip install --upgrade pip
RUN pip install awscli
RUN pip install cfn-lint
RUN pip install awscurl

ENV DOCKER_VERSION "18.06.1-ce"
RUN wget -q -P /tmp https://download.docker.com/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz \
  && tar -xz -C /tmp -f /tmp/docker-$DOCKER_VERSION.tgz \
  && mv /tmp/docker/docker /usr/bin \
  && rm -rf /tmp/docker /tmp/docker-$DOCKER_VERSION.tgz

RUN wget -O phpunit https://phar.phpunit.de/phpunit-7.phar \
  && chmod +x phpunit \
  && mv phpunit /usr/bin/phpunit