FROM phusion/baseimage

MAINTAINER Yu Shi <tttptd@yandex.com>

RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

# Install "software-properties-common" (for the "add-apt-repository")
RUN apt-get update && apt-get install -y software-properties-common

# Add the "PHP 7" ppa
RUN add-apt-repository -y ppa:ondrej/php

RUN add-apt-repository -y ppa:jonathonf/ffmpeg-4

# Install PHP-CLI 7.1, some PHP extentions and some useful Tools with APT
RUN apt-get update && apt-get install -y --force-yes \
        php7.2-cli \
        php7.2-imagick \
        php7.2-gd \
        php7.2-common \
        php7.2-curl \
        php7.2-json \
        php7.2-xml \
        php7.2-mbstring \
        # php7.2-mcrypt \ # https://serverpilot.io/docs/how-to-install-the-php-mcrypt-extension
        php7.2-mysql \
        php7.2-sqlite \
        php7.2-sqlite3 \
        php7.2-zip \
        php7.2-bcmath \
        php7.2-memcached \
        sqlite3 \
        libsqlite3-dev \
        # для запуска mysqldump
        mysql-client-5.7 \
        git \
        curl \
        vim \
        nano \
        ffmpeg

# Clean up, to free some space
RUN apt-get clean

# Add an alias for PHPUnit
RUN echo "alias phpunit='./vendor/bin/phpunit'" >> ~/.bashrc

# Install Composer
RUN curl -s http://getcomposer.org/installer | php \
    && mv ./composer.phar /usr/local/bin/ \
    && ln -s /usr/local/bin/composer.phar /usr/local/bin/composer \
    && echo "alias composer='/usr/local/bin/composer.phar'" >> ~/.bashrc

# ускоряет установку зависимостей посредством параллельного скачивания.
# https://habrahabr.ru/company/mailru/blog/346488/
RUN composer global require hirak/prestissimo

# Source the bash
RUN . ~/.bashrc

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

