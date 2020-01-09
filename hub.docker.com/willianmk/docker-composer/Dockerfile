FROM php:5.6-cli
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
    yes | pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    docker-php-ext-install pdo pdo_mysql && \
    apt-get update && apt-get install -y git --no-install-recommends && \
    rm -r /var/lib/apt/lists/*
WORKDIR /var/www
EXPOSE 8000/tcp
