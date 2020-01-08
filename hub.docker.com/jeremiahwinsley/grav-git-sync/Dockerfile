FROM php:7.2-apache

RUN apt-get update && apt-get install -y unzip git libpng-dev zlib1g-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install zip \
    && docker-php-ext-install gd

RUN a2enmod rewrite

ADD https://github.com/hibbitts-design/grav-skeleton-learn2-with-git-sync/releases/download/v1.1.0/grav-skeleton-learn2-with-git-sync-site.zip /tmp/grav-skeleton.zip

RUN mkdir /tmp/grav-skeleton \
    && rm -rf /var/www/html \
    && unzip -d /tmp/grav-skeleton /tmp/grav-skeleton.zip \
    && mv /tmp/grav-skeleton/grav-skeleton-learn2-with-git-sync-site /var/www/html \
    && rm -rf /tmp/grav-skeleton \
    && chown -R www-data:www-data /var/www/html
