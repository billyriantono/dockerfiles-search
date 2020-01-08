FROM php:7-fpm-stretch
LABEL maintainer=it-devops@pixartprinting.com
ARG COMPOSER_AUTH
ARG COMPOSER_ALLOW_SUPERUSER=1

RUN ln -snf /usr/share/zoneinfo/Europe/Rome /etc/localtime && \
    echo Europe/Rome > /etc/timezone && \
    apt-get update && \
    apt-get install -y \
    ca-certificates \
    supervisor \
    libzip-dev \
    git \
    procps \
    libicu-dev \
    libpng-dev && \
    docker-php-ext-install -j$(nproc) gd pdo pdo_mysql mysqli bcmath zip intl json opcache mbstring && \
    pecl install xdebug redis apcu && \
    docker-php-ext-enable redis apcu && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    apt-get remove gcc -y && \
    apt-get clean && \
    rm -fr /usr/local/etc/php-fpm.d && \
    rm -rf /var/lib/apt/lists/*

COPY cert.crt /tmp/cert.crt
RUN cp /tmp/cert.crt /usr/local/share/ca-certificates/ && \
    update-ca-certificates

COPY ./conf/php.ini /usr/local/etc/php/
COPY conf/php-fpm.conf /usr/local/etc/

COPY entrypoint.sh /bin/
RUN chmod 755 /bin/entrypoint.sh
ENTRYPOINT ["/bin/entrypoint.sh"]
WORKDIR /var/www
EXPOSE 9001
CMD ["php-fpm", "-R"]
