FROM php:7.2-cli

RUN apt-get update \
    && apt-get install -y \
        librabbitmq-dev \
        libssh-dev \
        libzip-dev \
    && docker-php-ext-install bcmath zip \
    && pecl install amqp \
    && docker-php-ext-enable amqp \
    && rm -rf /var/lib/apt/lists/*

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME=/opt/composer/
ENV PATH /opt/composer/bin:$PATH

COPY --from=composer:1.8 /usr/bin/composer /usr/bin/composer
