# Set the base image
FROM php:7.0.18-cli

# Dockerfile author / maintainer
MAINTAINER Evan Salzbrenner <hello@aboutevan.com>

# Updates
RUN apt-get update && apt-get install -y redis-server
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash
RUN apt-get update && apt-get -y install libpcre3-dev zlib1g-dev libbz2-dev libpng12-dev libjpeg-dev nodejs git zip unzip curl rsync mysql-client
RUN docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install zip bz2 gd mysqli pdo pdo_mysql

# Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "copy('https://composer.github.io/installer.sig', 'composer-setup.sig');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('composer-setup.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
RUN php -r "unlink('composer-setup.sig');"

# Install Node / Yarn
RUN npm -g install yarn

# WP CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp
RUN php -d memory_limit=512M /usr/local/bin/wp --allow-root package install git@github.com:schrapel/blade-generate.git
