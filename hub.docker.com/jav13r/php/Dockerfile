FROM php:5.6.35-cli

RUN apt-get update \
    && apt-get install -y \
    zip \
    unzip \
    curl \
    wget \
    nano \
    cron \
    git \
    mcrypt \
    libpq-dev \
    libmcrypt-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install mcrypt \
    && apt-get remove -y \
        libmcrypt-dev \
    && apt-get install -y \
        libmcrypt4 \
    && apt-get autoremove -y \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"
