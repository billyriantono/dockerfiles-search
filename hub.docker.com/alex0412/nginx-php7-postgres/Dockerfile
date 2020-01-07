FROM richarvey/nginx-php-fpm

MAINTAINER Alexander Li <a.li@playboy.de>

RUN rm /etc/nginx/sites-enabled/default.conf && rm /etc/nginx/sites-available/default.conf
ADD conf/symfony-app.conf /etc/nginx/sites-available/symfony-app.conf
RUN ln -s /etc/nginx/sites-available/symfony-app.conf /etc/nginx/sites-enabled/symfony-app.conf

RUN apk add --update --no-cache postgresql-dev && docker-php-ext-install pdo_pgsql
