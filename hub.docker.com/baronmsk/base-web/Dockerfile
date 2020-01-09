FROM ubuntu:xenial-20190122

ENV TERM=xterm \
    DEBIAN_FRONTEND=noninteractive

RUN set -ex && \
    apt-get update && \
    apt-get install --yes --no-install-recommends \
        apt-transport-https \
        apt-utils \
        ca-certificates \
        pkg-config && \
    apt-get upgrade --yes && \
    \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 && \
    echo "deb [arch=amd64] https://nginx.org/packages/ubuntu/ xenial nginx" > /etc/apt/sources.list.d/nginx.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C && \
    echo "deb [arch=amd64] http://ppa.launchpad.net/ondrej/php/ubuntu xenial main" > /etc/apt/sources.list.d/php.list && \
    \
    apt-get update && \
    ACCEPT_EULA=Y apt-get install --yes --no-install-recommends \
        curl \
        freetds-bin \
        locales \
        nginx \
        php7.2-amqp \
        php7.2-apcu \
        php7.2-bcmath \
        php7.2-cli \
        php7.2-common \
        php7.2-curl \
        php7.2-dev \
        php7.2-imagick \
        php7.2-intl \
        php7.2-fpm \
        php7.2-gd \
        php7.2-json \
        php7.2-mbstring \
        php7.2-memcache \
        php7.2-memcached \
        php7.2-mysql \
        php7.2-opcache \
        php7.2-readline \
        php7.2-redis \
        php7.2-soap \
        php7.2-sybase \
        php7.2-xml \
        php7.2-zip \
        supervisor \
        tzdata && \
    \
    locale-gen --purge en_US.UTF-8 && update-locale LANG=en_US.UTF-8 && \
    echo 'Europe/Moscow' > /etc/timezone && \
    cp -vf /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
    \
    apt-get autoremove --yes make php7.2-dev && \
    apt-get clean && \
    cd / && \
    rm -rf \
        /tmp/* \
        /var/lib/apt/lists/* \
        /etc/filebeat/* \
        /etc/nginx/conf.d/* \
        /etc/php/5.* \
        /etc/php/7.{0,2} \
        /var/www/* && \
    chown root:root /tmp && chmod 1777 /tmp

COPY assets /etc

EXPOSE 80

WORKDIR /var/www

ENTRYPOINT ["supervisord", "--nodaemon"]
