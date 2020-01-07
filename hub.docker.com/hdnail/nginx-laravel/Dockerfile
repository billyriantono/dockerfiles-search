FROM debian:jessie-slim

MAINTAINER Damian Nail <hdnail@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ENV PHP_DISPLAY_ERRORS Off
ENV PHP_LOG_ERRORS Off
ENV PHP_MEMORY_LIMIT 256M
ENV PHP_UPLOAD_MAX_FILESIZE 50M
ENV PHP_POST_MAX_SIZE 50M
ENV DEFAULT_TIMEZONE Europe/London

# Config scripts.
COPY ./dockerfiles/nginx-laravel-base.sh /nginx-laravel-base.sh
COPY ./dockerfiles/nginx-laravel-entrypoint.sh /nginx-laravel-entrypoint.sh
COPY ./dockerfiles/nginx.conf /etc/nginx/sites-available/default.conf

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        curl \
        locales \
        lsb-release \
        openssl \
        wget \
        zip \
        unzip && \

    # PHP 7.2 libraries.
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list' && \
    apt-get update && \
    apt-get install -y --no-install-recommends \
        php7.2 \
        php7.2-common \
        php7.2-cgi \
        php7.2-cli \
        php7.2-curl \
        php7.2-fpm \
        php7.2-intl \
        php7.2-json \
        php7.2-mbstring \
        php7.2-xml \
        php7.2-zip && \

    rm -f /etc/apt/sources.list.d/php.list && \

    # NginX
    apt-get update && \
    apt-get install -y --no-install-recommends \
        nginx \
        nginx-extras && \

    # Composer install.
    cd ~ && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer && \

    # Volume config.
    mkdir -p /var/www/html && \
    chown www-data:www-data /var/www/html && \

    # PHP-FPM folder config.
    mkdir -p /run/php && \
    chown www-data:www-data /run/php && \
    mkdir -p /etc/php/7.2/conf && \

    # NGINX logging.
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log && \

    # Image cleaning.
    apt-get -y autoremove && \
    apt-get -y autoclean && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* /var/tmp/* && \

    # Configuration setup.
    cd /etc/nginx/sites-enabled && \
    rm -f * && \
    ln -s ../sites-available/default.conf default.conf && \
    chmod a+x \
        /nginx-laravel-base.sh \
        /nginx-laravel-entrypoint.sh

VOLUME ["/var/www/html"]

WORKDIR "/var/www/html"

ENTRYPOINT ["/nginx-laravel-entrypoint.sh"]

EXPOSE 80

CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
