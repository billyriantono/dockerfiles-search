FROM php:7.2-cli
RUN apt-get update && apt-get -y install libxml2-dev unzip
RUN docker-php-ext-install soap
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
CMD ["composer"]
