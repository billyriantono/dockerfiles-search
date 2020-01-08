FROM ubuntu:18.04

ENV  LANG="en_US.UTF-8" \
     LC_ALL="en_US.UTF-8" \
     LANGUAGE="en_US.UTF-8" \
     TERM="xterm" \
     DEBIAN_FRONTEND="noninteractive" \
     COMPOSER_ALLOW_SUPERUSER=1

RUN apt-get update -q && \
    apt-get install -qy software-properties-common language-pack-en-base && \
    export LC_ALL=en_US.UTF-8 && \
    export LANG=en_US.UTF-8

RUN apt-get install --no-install-recommends -qy \
    ca-certificates \
    curl \
    nginx \
    git \
    php \
    php-curl \
    php-fpm \
    php-gd \
    php-intl \
    php-mbstring \
    php-pdo \
    php-zip \
    php-xml \
    php-mysql \
    php-ldap \
    php-bcmath \
    php-iconv \
    php-soap \
    supervisor \
    bzip2 \
    unzip

RUN cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime && echo "Europe/Moscow" > /etc/timezone && \

    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \

    curl -sL https://deb.nodesource.com/setup_8.x | bash && apt-get install -y nodejs && \

    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update -q && apt-get install --no-install-recommends -qy yarn

RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && mkdir /run/php

COPY php.ini /etc/php/7.2/cli/conf.d/50-setting.ini
COPY php.ini /etc/php/7.2/fpm/conf.d/50-setting.ini
COPY pool.conf /etc/php/7.2/fpm/pool.d/www.conf

COPY nginx.conf /etc/nginx/nginx.conf
# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

COPY supervisord.conf /etc/supervisor/supervisord.conf

EXPOSE 80 443
WORKDIR /app


CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
