FROM php:7-cli-alpine3.9
LABEL Ludwring Liccien <ludwring.liccien@gmail.com>

RUN apk add --update alpine-sdk sudo git bash nano

RUN apk add --no-cache libpng libpng-dev && docker-php-ext-install gd && apk del libpng-dev

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

# Create user
RUN adduser -S appuser -G root

RUN chown -R appuser:root /usr/local/bin
# Tell docker that all future commands should run as the appuser user
USER appuser

WORKDIR /app

ENTRYPOINT [ "composer" ]
CMD [ "list" ]