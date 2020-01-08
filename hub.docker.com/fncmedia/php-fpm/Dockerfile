FROM php:7.2-fpm

ENV APPLICATION_NAME web-application

# Install dependencies
RUN apt-get update && apt-get install -y \
      ca-certificates \
      libicu-dev \
      libpng-dev \
      libjpeg-dev \
      libxml2 \
      libxml2-dev \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libmcrypt-dev \
      libpq-dev \
      libcurl3 \
      libcurl3-dev \
      libpng-dev \
      bzip2 \
      curl \
      wget \
      locales \
      libssl-dev \
      zlib1g-dev \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen \
    && locale-gen

# Environment Layer
RUN pecl install \
      mongodb \
      apcu \
      redis \
    && pecl upgrade mongodb \
    && docker-php-ext-enable \
      mongodb \
      apcu \
      redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-install -j$(nproc) \
        zip \
        intl \
        mbstring \
        exif \
        bcmath \
        pdo \
        pdo_mysql \
        pdo_pgsql \
        pgsql \
        curl \
        opcache \
        iconv \
        mcrypt \
        soap \
    && docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# Added local Cache and Log Directory
RUN mkdir -p \
      /var/cache/${APPLICATION_NAME} \
      /var/log/${APPLICATION_NAME} \
    && chmod 777 \
      /var/cache/${APPLICATION_NAME} \
      /var/log/${APPLICATION_NAME}

RUN usermod -u 1000 www-data

VOLUME /var/www/${APPLICATION_NAME}

WORKDIR /var/www/${APPLICATION_NAME}
