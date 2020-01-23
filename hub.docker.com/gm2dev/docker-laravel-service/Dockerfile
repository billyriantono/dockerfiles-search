#Tomamos la imagen de php fpm para utilizar las librerias compiladas
FROM php:7.2-fpm-stretch

#Instalamos nginx y otras dependencias del framework
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    wget \
    lsb-release \
    libxml2-dev \
    nginx \
    ca-certificates \
    git \
    zip

#Compilamos pgsql
RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

#Compilamos las librerias requeridas por laravel
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install xml
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install pcntl

#Install supervisor porque debemos tener dos procesos, nginx y fpm
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list

RUN apt-get update && apt-get install -y \
    supervisor \
    curl \
    libssl-dev \
    libmcrypt-dev

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === '48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"
