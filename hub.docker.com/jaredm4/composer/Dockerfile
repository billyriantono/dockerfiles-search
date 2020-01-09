
FROM php:5.6-cli

# Composer dependencies
RUN apt-get update \
    && apt-get install -y zlib1g-dev libbz2-dev mercurial git subversion \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY php.ini /usr/local/etc/php/

RUN docker-php-ext-install bz2 zip

# Composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer --version=1.0.0-alpha10
ENTRYPOINT ["composer"]

