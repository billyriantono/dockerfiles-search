
FROM php:7.3-cli

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
      locales \
      ghostscript

RUN apt-get update && apt-get install -yq --no-install-recommends \
    mysql-client \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN docker-php-ext-install pdo pdo_mysql

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Set locales
RUN locale-gen en_US.UTF-8 en_GB.UTF-8 de_DE.UTF-8 es_ES.UTF-8 fr_FR.UTF-8 it_IT.UTF-8

# Default to UTF-8 file.encoding
ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    LANGUAGE=C.UTF-8

WORKDIR /var/www/html

ENTRYPOINT []