FROM ubuntu:14.04

MAINTAINER Kristof Coomans "kristof@2dotstwice.be"
ENV REFRESHED_AT "2017-02-25 07:06:00"

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing --no-install-recommends -q install \
        software-properties-common && \
    LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php && \
    DEBIAN_FRONTEND=noninteractive apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing --no-install-recommends -q install \
        php7.0-cli \
        php7.0-gd \
        php7.0-sqlite \
        php7.0-mysqlnd \
        php7.0-curl \
        php7.0-intl \
        php7.0-xml \
        php7.0-mbstring \
        php7.0-json \
        php7.0-mcrypt \
        php7.0-bcmath \
        php7.0-soap \
        php7.0-zip && \
    rm -rf /var/lib/apt/lists/*

CMD /bin/bash
