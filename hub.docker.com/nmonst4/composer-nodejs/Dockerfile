FROM php:7.2-fpm

RUN apt update && \
  apt install -y apt-transport-https build-essential gnupg git zip unzip openssl libssl-dev zlib1g-dev libzip-dev
    
RUN docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/ && \
    ln -s /usr/local/bin/composer.phar /usr/local/bin/composer

# Install Node.js & Yarn
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt install -y nodejs
