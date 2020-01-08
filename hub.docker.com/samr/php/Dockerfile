FROM php:7.2-fpm

RUN apt-get update -y && apt-get install -y \
    openssl zip unzip git libpq-dev libpng-dev
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql mbstring bcmath gd zip

#Can be removed when all packages have composer and npm installed through Dockerfile!
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

COPY run.sh /run.sh
RUN chmod +x /run.sh

EXPOSE 9000

ENTRYPOINT ["/run.sh"]

