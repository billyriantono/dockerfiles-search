FROM php:7.2.13-cli-alpine3.8

LABEL "maintainer"="Ahmad Mayahi <ahmad.mayahi@gmail.com>"

RUN apk update && \
    apk add --no-cache zlib-dev rsync openssh-client && \
    docker-php-ext-install -j$(nproc) mysqli pdo_mysql zip && \
    wget -O - https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["docker-php-entrypoint"]
CMD ["php", "-a"]
