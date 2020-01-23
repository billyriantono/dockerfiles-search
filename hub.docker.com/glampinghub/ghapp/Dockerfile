# Copyright (C) 2020 Glamping Hub (https://glampinghub.com)
# All rights reserved

FROM ubuntu:bionic

ENV DEBIAN_FRONTEND=noninteractive \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    TERM=${TERM:-xterm} \
    PORT=8000 \
    ENV=develop \
    PATH=/webapp/venv/bin/:/webapp/.venv/bin/:$PATH \
    DEBUG=True

ADD https://deb.nodesource.com/setup_10.x /tmp/setup-nodejs
COPY ./sd_notify /usr/bin/
COPY ./docker-entrypoint.sh /
COPY ./http_ok-linux-amd64 /usr/local/bin/http_ok

RUN apt-get update \
    && apt-get install locales \
    && locale-gen en_US.UTF-8 \
    && echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections \
    && bash /tmp/setup-nodejs \
    && apt-get install --no-install-recommends -qy \
        nodejs openssh-client git \
        build-essential awscli \
        virtualenv python3 python3-dev python3-pip python3-setuptools python3-wheel \
        libpq-dev libmaxminddb0 libmaxminddb-dev libmemcached-dev \
        libjpeg8 libjpeg8-dev libopenjp2-7 libopenjp2-7-dev libtiff5 libtiff5-dev \
        libfreetype6 libfreetype6-dev libwebp6 libwebp-dev \
        libgeos-3.6.2 libgeos-dev gdal-bin libgdal-dev python3-gdal binutils libproj-dev \
        wkhtmltopdf xvfb \
        libffi-dev \
        vim nano less jq \
        libssl-dev default-libmysqlclient-dev \
        && ln -s /usr/include/freetype2 /usr/local/include/freetype \
    && echo -n '#!/bin/sh\nxvfb-run -a /usr/bin/wkhtmltopdf "$@" || /usr/bin/wkhtmltopdf "$@"\n' > /usr/local/bin/wkhtmltopdf \
    && chmod +x /usr/local/bin/wkhtmltopdf \
    && npm install --global --production eslint \
    && update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1 \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3.6 1 \
    && update-alternatives --install /usr/bin/python python /usr/bin/python2.7 2 \
    && update-alternatives --set python /usr/bin/python3.6 \
    && pip install flake8 flake8_formatter_junit_xml \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /webapp
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/bin/sleep","infinity"]

# Metadata
LABEL org.opencontainers.image.authors="José Luis Salvador Rufo <salvador.joseluis@gmail.com>" \
      org.opencontainers.image.title="Django container" \
      org.opencontainers.image.url="https://glampinghub.com" \
      org.opencontainers.image.vendor="Glamping Hub USA Inc."