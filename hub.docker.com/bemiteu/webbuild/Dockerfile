#
# Docker Image for WebBuilds in BitBucket Pipelines

FROM ubuntu:18.04

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get upgrade -y

RUN apt-get install -yq --no-install-recommends \
      gnupg2 \
      curl \
      apt-utils \
      build-essential \
      software-properties-common \
      wget \
      git \
      openssl \
      iputils-ping \
      net-tools \
      ant \
      rsync \
      ssh-client \
      ssh \
      lftp \
      unzip \
      zip \
      locales \
      ghostscript \
      imagemagick

# Install Handbrake
RUN add-apt-repository --yes ppa:stebbins/handbrake-releases \
    && apt-get update -qq \
    && apt-get install -qq handbrake-cli

# Install NodeJS + NPM through nvm
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

ENV NVM_DIR=/root/.nvm
RUN . $HOME/.nvm/nvm.sh \
    && nvm install 8.9.4 \
    && nvm install 8.14.1 \
    && nvm install 10.14.2 \
    && nvm alias default 10.14.2 \
    && nvm use default

# PHP Repo
RUN add-apt-repository ppa:ondrej/php

# Yarn Repo
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install PHP, Yarn, runtime things
RUN apt-get update && apt-get install -yq --no-install-recommends \
    php7.4 php7.4-fpm \
    php7.4-common php7.4-cli php7.4-mbstring php7.4-bcmath php7.4-curl php7.4-imap \
    php7.4-mysql php7.4-pdo php7.4-pgsql \
    php7.4-opcache \
    php7.4-gd php7.4-imagick \
    php7.4-intl php7.4-readline php7.4-pspell php7.4-tidy php7.4-xsl \
    php7.4-apc php7.4-memcached \
    php7.4-xml php7.4-zip php7.4-json \
    php-redis \
    php-mongodb \
    php-msgpack \
    php-ssh2 \
    php-yaml \
    php-zmq \
    php-imagick \
    mysql-client \
    sqlite3 \
    yarn \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set locales
RUN locale-gen en_US.UTF-8 en_GB.UTF-8 de_DE.UTF-8 es_ES.UTF-8 fr_FR.UTF-8 it_IT.UTF-8

# Default to UTF-8 file.encoding
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    LANGUAGE=C.UTF-8

# Create dirs and users
RUN mkdir -p /opt/bemiteu/build/

# atlassian pipelines are running in:
# /opt/atlassian/pipelines/agent/build
WORKDIR /opt/bemiteu/build

# Copy buildTool and make scripts available through PATH
COPY buildTool ./buildTool

RUN find /opt/bemiteu -type d -exec chmod 755 {} \;

ENV PATH="/opt/bemiteu/build/buildTool:${PATH}"

RUN find /opt/bemiteu/build/buildTool -type f -exec chmod 755 {} \;


ENTRYPOINT /bin/bash
