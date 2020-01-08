FROM php:7.1-fpm
MAINTAINER Maciej Krawczyk <wirus15@gmail.com>

COPY ./php.ini /usr/local/etc/php/php.ini

RUN apt-get update
RUN apt-get dist-upgrade -y
RUN apt-get install -y git curl nano zlib1g-dev

# install extensions
RUN docker-php-ext-install zip mbstring pdo_mysql

# install composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
