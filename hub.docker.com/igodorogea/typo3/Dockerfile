FROM igodorogea/ubuntu-nginx-php:latest

LABEL maintainer="Ivan Godorogea"

ENV DEBIAN_FRONTEND=noninteractive

RUN rm -rf /var/www/html/*

ADD files/etc/nginx/sites-available/default /etc/nginx/sites-available/default
ADD files/var/www/html/config /var/www/html/config
ADD files/var/www/html/packages /var/www/html/packages
ADD files/var/www/html/var /var/www/html/var

# Fix permisions broken by windows FS
RUN chmod -x /etc/nginx/sites-available/default \
 && ln -s /var/www/html/config/.env /var/www/html/.env \
 && ln -s /var/www/html/config/composer.json /var/www/html/composer.json \
 && ln -s /var/www/html/config/composer.lock /var/www/html/composer.lock \
 && find /var/www/html -type d -exec chmod 755 {} \; \
 && find /var/www/html -type f -exec chmod 644 {} \; \
 && composer install \
 && rm -rf ~/.composer/cache/* \
 && chown -R www-data: /var/www
