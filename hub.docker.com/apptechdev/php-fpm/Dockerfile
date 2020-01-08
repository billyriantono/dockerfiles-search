FROM php:5-fpm

ENV DEBIAN_FRONTEND "noninteractive"
ENV NR_INSTALL_SILENT 1
ENV NR_INSTALL_PHPLIST "/usr/local/bin"
ENV NR_INSTALL_KEY "3785383d600498917d272a2715204e8b5a3a1927"
ENV APP_USER "www-data"
ENV APP_ROOT "/var/www/app"
ENV APP_LOGS "/var/log/app"

WORKDIR /tmp

RUN apt-get update -qq && \
    apt-get install -yq \
        build-essential \
        git \
        netcat \
        python \
        rsync \
        wget \
        zip

RUN wget -O - https://download.newrelic.com/548C16BF.gpg | apt-key add -  && \
    sh -c 'echo "deb http://apt.newrelic.com/debian/ newrelic non-free" > /etc/apt/sources.list.d/newrelic.list'  && \
    apt-get update  && \
    apt-get install -yq newrelic-php5 && \
    newrelic-install install

RUN curl -s "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" && \
    unzip ./awscli-bundle.zip && \
    ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

RUN curl -sS "https://getcomposer.org/installer" | php && \
    mv ./composer.phar /usr/local/bin/composer

RUN mkdir -p /usr/src/php/ext && \
    mkdir -p $APP_LOGS && \
    chown -R $APP_USER:$APP_USER $APP_LOGS

RUN apt-get autoremove -yq && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/www/*

COPY ./php-fpm.d /usr/local/etc/php-fpm.d
COPY ./php /usr/local/etc/php

WORKDIR $APP_ROOT
