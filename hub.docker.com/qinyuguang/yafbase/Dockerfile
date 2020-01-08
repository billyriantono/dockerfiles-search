FROM php:latest

MAINTAINER Qin Yuguang <qinyuguang@gmail.com>

RUN docker-php-ext-install pdo_mysql pcntl \
    && pecl install yaf \
    && pecl clear-cache \
    && apt-get update \
    && apt-get install -y cron \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* \
    && sed -i '/session    required     pam_loginuid.so/c\#session    required     pam_loginuid.so' /etc/pam.d/cron
