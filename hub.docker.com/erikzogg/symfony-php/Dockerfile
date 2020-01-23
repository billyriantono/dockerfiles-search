FROM php:7.3-fpm

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl wget zip unzip \
    libxml2 libxml2-dev libicu-dev libzip-dev

RUN docker-php-ext-install -j$(nproc) intl opcache pdo_mysql mysqli

RUN docker-php-ext-configure zip --with-libzip
RUN docker-php-ext-install -j$(nproc) zip

RUN pecl install apcu
RUN pecl install apcu_bc
RUN docker-php-ext-enable apcu --ini-name 10-docker-php-ext-apcu.ini
RUN docker-php-ext-enable apc --ini-name 20-docker-php-ext-apc.ini

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version

RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony \
    && chmod a+x /usr/local/bin/symfony \
    && symfony --version

RUN curl -sL https://deb.nodesource.com/setup_12.x | bash \
    && apt-get install -y --no-install-recommends nodejs \
    && node -v && npm -v

RUN npm install -g yarn && yarn --version

RUN curl --location --output /usr/local/bin/phpcs https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar \
    && chmod +x /usr/local/bin/phpcs

RUN curl --location --output /usr/local/bin/phpstan https://github.com/phpstan/phpstan/releases/download/0.11.12/phpstan.phar \
    && chmod +x /usr/local/bin/phpstan

RUN curl --location --output /usr/local/bin/phpunit https://phar.phpunit.de/phpunit.phar \
    && chmod +x /usr/local/bin/phpunit
