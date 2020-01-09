FROM php:7.0.1-apache
ADD config/php/php.ini /usr/local/etc/php/
RUN docker-php-ext-install mbstring pdo_mysql
RUN docker-php-ext-configure mbstring
RUN docker-php-ext-configure pdo_mysql
RUN docker-php-ext-enable mbstring pdo_mysql
RUN a2enmod rewrite && service apache2 restart
