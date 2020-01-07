FROM wordpress:latest

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev; \
    docker-php-ext-install zip

COPY uploads.ini /usr/local/etc/php/conf.d/uploads.ini

CMD ["apache2-foreground"]
