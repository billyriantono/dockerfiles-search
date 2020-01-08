FROM prestashop/base:7.0-fpm

MAINTAINER Lukas Cerny <lukas.cerny@futuretek.cz>

ENV PS_VERSION 1.7.4.2

# Get PrestaShop
ADD https://www.prestashop.com/download/old/prestashop_1.7.4.2.zip /tmp/prestashop.zip

# Extract
RUN mkdir -p /tmp/data-ps \
	&& unzip -q /tmp/prestashop.zip -d /tmp/data-ps/ \
	&& bash /tmp/ps-extractor.sh /tmp/data-ps \
	&& rm /tmp/prestashop.zip

COPY ./etc /etc

RUN sed -i 's|memory_limit = 128M|memory_limit = 512M|g' /usr/local/etc/php/php.ini

RUN sed -i 's|#!/bin/sh|#!/bin/sh\ncron;\nln -sf /root/cron/crontab /etc/crontab;|g' /tmp/docker_run.sh \
    && mkdir /root/cron \
    && touch /etc/crontab
