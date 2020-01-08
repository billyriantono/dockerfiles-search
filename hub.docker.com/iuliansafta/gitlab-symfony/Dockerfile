FROM php:7.1-fpm
RUN apt-get update \
        && mkdir -p /usr/share/man/man1 \
        && mkdir -p /usr/share/man/man7 \
        && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libpq-dev \
        postgresql \
        postgresql-contrib \
        libxml2-dev \
        git \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pdo pdo_pgsql \
    && docker-php-ext-install -j$(nproc) bcmath mbstring json xml xmlrpc zip intl opcache

ENV WORKDIR "/var/www/app"

# Add timezone
RUN ln -snf /usr/share/zoneinfo/Europe/Paris /etc/localtime

# Install composer
RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir -p ${WORKDIR}
RUN chown www-data:www-data -R ${WORKDIR}

WORKDIR ${WORKDIR}

EXPOSE 9000

CMD ["php-fpm"]
