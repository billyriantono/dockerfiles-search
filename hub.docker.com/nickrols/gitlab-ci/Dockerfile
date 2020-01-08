FROM php:7.3-fpm


# Install the PHP pdo_mysql extention
RUN docker-php-ext-install pdo_mysql
    
# Install Xdebug
#RUN pecl install xdebug && docker-php-ext-enable xdebug
#COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Install ZIP
# RUN pecl install zip && docker-php-ext-enable zip

# Install composer
# RUN curl -sS https://getcomposer.org/installer | php
# RUN mv composer.phar /usr/local/bin/composer

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
