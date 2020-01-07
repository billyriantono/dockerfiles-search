FROM wordpress:latest

RUN apt update \
    && apt install -y libxml2-dev \
    && apt install -y libzip-dev \
    && docker-php-ext-configure soap --enable-soap \
    && docker-php-ext-install soap \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip
