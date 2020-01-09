FROM php:7.1-fpm

COPY html /var/www/html
RUN mkdir -p /var/www/html/bundles \
    && echo "html{background:black;color:white}" > /var/www/html/bundles/style.css \
    && chown -R www-data:www-data /var/www

VOLUME /var/www/html/bundles
