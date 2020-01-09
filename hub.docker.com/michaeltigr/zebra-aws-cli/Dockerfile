FROM python:2-alpine

LABEL maintainer "Michael Molchanov <mmolchanov@adyax.com>"

USER root

# SSH config.
RUN mkdir -p /root/.ssh
ADD config/ssh /root/.ssh/config
RUN chmod 600 /root/.ssh/config

# Install base.
RUN apk add --update --no-cache \
  bash \
  build-base \
  curl \
  git \
  groff \
  less \
  libffi \
  libffi-dev \
  mysql-client \
  openssh \
  openssl \
  openssl-dev \
  procps \
  postgresql-client \
  rsync \
  tar \
  unzip \
  wget \
  &&  rm -rf /var/lib/apt/lists/*

# Install aws-cli.
RUN pip install awscli s3cmd python-magic
