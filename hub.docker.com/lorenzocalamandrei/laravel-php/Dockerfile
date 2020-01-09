FROM php:7.2.23-fpm

LABEL mantainer="Lorenzo Calamandrei <nexcal.dev@gmail.com>"

# user 1000
RUN mkdir /home/local \
    && useradd -u 1000 local -d "/home/local" \
    && chown local.local /home/local

# update
RUN apt-get update -y && apt-get upgrade -y

RUN apt-get install -y --no-install-recommends apt-utils zip zlib1g-dev libxml2-dev libssl-dev > /dev/null

# composer
RUN apt-get install curl > /dev/null && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# laravel deps
RUN docker-php-ext-configure zip > /dev/null && docker-php-ext-install zip > /dev/null
RUN docker-php-ext-configure bcmath > /dev/null && docker-php-ext-install bcmath > /dev/null
RUN docker-php-ext-configure ctype > /dev/null && docker-php-ext-install ctype > /dev/null
RUN docker-php-ext-configure json > /dev/null && docker-php-ext-install json > /dev/null
RUN docker-php-ext-configure mbstring > /dev/null && docker-php-ext-install mbstring > /dev/null
RUN docker-php-ext-configure pdo > /dev/null && docker-php-ext-install pdo > /dev/null
RUN docker-php-ext-configure pdo_mysql > /dev/null && docker-php-ext-install pdo_mysql > /dev/null
RUN docker-php-ext-configure tokenizer > /dev/null && docker-php-ext-install tokenizer > /dev/null
RUN docker-php-ext-configure simplexml > /dev/null && docker-php-ext-install simplexml > /dev/null
RUN docker-php-ext-configure xml > /dev/null && docker-php-ext-install xml > /dev/null

USER 1000
RUN composer global require laravel/installer
RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc
