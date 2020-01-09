FROM composer

RUN apk add icu-dev \
    && docker-php-ext-install bcmath intl pcntl pdo_mysql \
    && rm -rf /var/cache/apk/*
