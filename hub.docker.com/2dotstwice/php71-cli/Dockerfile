FROM ubuntu:14.04

MAINTAINER Kristof Coomans "kristof@2dotstwice.be"
ENV REFRESHED_AT "2017-02-17 08:08:00"

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing --no-install-recommends -q install \
        software-properties-common && \
    LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php && \
    DEBIAN_FRONTEND=noninteractive apt-get -y update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing --no-install-recommends -q install \
        php7.1-cli \
        php7.1-gd \
        php7.1-sqlite \
        php7.1-mysqlnd \
        php7.1-curl \
        php7.1-intl \
        php7.1-xml \
        php7.1-mbstring \
        php7.1-json \
        php7.1-mcrypt \
        php7.1-bcmath \
        php7.1-soap \
        php7.1-zip && \
    rm -rf /var/lib/apt/lists/*

CMD /bin/bash
