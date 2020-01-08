FROM php:5.6-fpm

ENV LANG C.UTF-8
ENV TZ=Europe/Moscow
ENV SUPPORTED_LANGUAGES="en_US.UTF-8|ru_RU.UTF-8"

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# php exts deps
RUN apt-get update \
    && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libmcrypt-dev \
    && docker-php-ext-install -j$(nproc) \
        mcrypt \
        gettext \
        gd \
        pcntl \
        zip \
        bcmath \
        opcache \
        pdo \
    && pecl install apcu-4.0.11 \
    && docker-php-ext-enable apcu \
    && apt-get remove -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng12-dev \
        libmcrypt-dev \
    && apt-get install -y \
        libfreetype6 \
        libjpeg62-turbo \
        libpng12-0 \
        libmcrypt4 \
    && apt-get -y autoclean && apt-get -y autoremove && apt-get -y clean

# additional soft
RUN apt-get install -y git subversion supervisor && \
    apt-get clean && \
    curl --insecure https://getcomposer.org/composer.phar -o /usr/bin/composer && chmod +x /usr/bin/composer

# locales
RUN \
  apt-get install locales && \
  cat /usr/share/i18n/SUPPORTED | grep -E "$SUPPORTED_LANGUAGES" > /etc/locale.gen && \
  locale-gen  && \
  apt-get -y autoclean && apt-get -y autoremove && apt-get -y clean

COPY wait-for-it.sh /usr/local/bin/wait-for-it
COPY php_overrides.ini /usr/local/etc/php/conf.d/zz-docker.ini
# COPY fpm.conf /usr/local/etc/php-fpm.d/zz-www-override.conf
COPY cli-entrypoint /usr/local/bin/cli-entrypoint