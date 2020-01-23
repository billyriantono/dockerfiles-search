FROM php:7.0-apache

RUN set -ex; \
        apt-get update && apt-get install -y \
        zlib1g-dev \
        libpq-dev \
        wget \
        unzip \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install \
        zip \
        pgsql \
        pdo_pgsql \
        mysqli \
        pdo_mysql

COPY fs-set.sh /usr/local/bin/

ENTRYPOINT [ "fs-set.sh" ]

CMD [ "apache2-foreground" ]