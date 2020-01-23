FROM ubuntu:18.04
USER root
ENV DEBIAN_FRONTEND noninteractive
ADD docker/scripts/startup.sh /data/scripts/startup.sh
ADD basic /data/www/basic
ADD hana /data/libs/hana
RUN apt-get update \
    && apt-get install -y --no-install-recommends software-properties-common \
    && export LC_ALL=C.UTF-8 \
    && apt-get update && apt-get install -y --no-install-recommends \
    wget \
    php \
    php-fpm \
    php-curl \
    php-mysql \
    php-mbstring \
    php-cli \
    php-dom \
    php-odbc \
    php-pdo-odbc \
    unzip \
    libaio-dev \
    nginx \
    && mkdir -p /data \
    && mkdir -p /data/scripts \
    && mkdir -p /data/libs \
    && mkdir -p /data/libs/composer \
    && mkdir -p /data/www/basic \
    && mkdir -p /etc/nginx/conf.d \
    && rm -rf /etc/nginx/conf.d/* \
    && rm -rf /var/lib/apt/lists/* \
    && wget --no-check-certificate -O composer-setup.php https://getcomposer.org/installer \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && cd /data/www/basic \
    && composer install \
    && cd /data/libs/hana \
    && tar -xvf rclient120_linux_x64.tgz \
    && ./hdbinst -a client \
    && chmod -R 777 /data/www/basic/runtime \
    && chmod -R 777 /data/www/basic/web \
    && chmod -R 777 /data/www/basic/web/assets \
    && chmod +x /data/scripts/startup.sh
ADD docker/config/nginx.conf /etc/nginx/nginx.conf
ADD docker/config/default.nginx.conf /etc/nginx/conf.d
EXPOSE 80
ENTRYPOINT ["/data/scripts/startup.sh"]
