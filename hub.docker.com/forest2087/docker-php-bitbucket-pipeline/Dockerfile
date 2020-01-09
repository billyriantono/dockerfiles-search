From php:5.6.37

RUN apt-get update && apt-get install -y unzip zip git
RUN pecl install xdebug-2.5.5 && docker-php-ext-enable xdebug
RUN docker-php-ext-install mysqli pdo pdo_mysql
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
