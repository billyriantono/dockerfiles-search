FROM php:7.1-fpm
RUN cd /tmp \
    && apt-get update \
    && mkdir -p /usr/share/man/man1 \
    && mkdir -p /usr/share/man/man7 \
    && apt-get install -y \
        libmcrypt-dev \
        libpq-dev \
        postgresql-client \
        libmagickwand-dev --no-install-recommends \
        zip \
        libxml2-dev \
        libcurl3-dev \
        libedit-dev \
        git \

    && docker-php-ext-install -j$(nproc) mcrypt gd pdo_pgsql zip curl bcmath opcache simplexml xmlrpc xml soap mbstring \

    # composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version \

    # xdebug
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \

    && apt-get autoremove -y \
        && apt-get autoclean -y \
        && apt-get clean -y \
        && rm -rf \
            /var/lib/apt/lists/* \
            /tmp/* \
            /var/tmp/* \
            /etc/php5 \
            /etc/php/5* \
            /var/log \
            /var/cache