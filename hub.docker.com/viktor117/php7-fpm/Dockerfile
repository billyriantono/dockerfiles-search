FROM php:7-fpm
MAINTAINER Viktor Tverdun <v.tverdun@gmail.com>

RUN apt-get update && apt-get -y install libmcrypt-dev unzip zlib1g-dev
RUN docker-php-ext-install pdo_mysql bcmath mbstring zip

# Install Redis extension
RUN pecl install redis
RUN docker-php-ext-enable redis

# Install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

# Install Nodejs and npm
RUN apt-get install -y gnupg gnupg1 gnupg2
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs build-essential

RUN groupadd -r docker && useradd -ms /bin/bash -g docker docker
