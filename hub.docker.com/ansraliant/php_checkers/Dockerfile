FROM php:7.3-cli-stretch

COPY composer-install.sh /root/composer-install.sh

RUN apt-get update && \
    apt-get install -y \
    wget \
    git \
    zip \
    unzip \
    zlib1g-dev \
    libzip-dev

RUN docker-php-ext-configure zip && docker-php-ext-install -j1 zip

RUN /root/composer-install.sh

ENV PATH="/root/.composer/vendor/bin:${PATH}"

RUN composer global require friendsofphp/php-cs-fixer && \
    composer global require phpmd/phpmd
