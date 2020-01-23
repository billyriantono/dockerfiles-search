FROM php:7.3-apache AS phpBase

COPY conf/000-default.conf /etc/apache2/sites-available/000-default.conf

WORKDIR /var/www/html

CMD chown -R www-data:www-data var && apachectl -DFOREGROUND

#build time
FROM phpBase AS build

COPY --from=composer /usr/bin/composer /usr/local/bin/composer
ENV COMPOSER_ALLOW_SUPERUSER=1

RUN apt update\
  && apt install -y unzip git\
  && rm -rf /var/lib/apt/lists/*

COPY src .

RUN composer install

#run time
FROM phpBase as prod

COPY --from=build /var/www/html .