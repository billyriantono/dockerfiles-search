
FROM node:11.10-stretch-slim

RUN apt-get update && apt-get install -yq --no-install-recommends \
      gnupg2 \
      curl \
      vim \
      nano \
      apt-utils \
      build-essential \
      software-properties-common \
      wget \
      git \
      openssl \
      iputils-ping \
      net-tools \
      rsync \
      ssh-client \
      ssh \
      lftp \
      unzip \
      zip \
      apt-transport-https \
      ca-certificates \
      ghostscript

RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

WORKDIR /var/www/html