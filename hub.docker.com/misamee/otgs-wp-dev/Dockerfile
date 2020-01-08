FROM php:5.6-apache

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libmysqlclient-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install opcache \
    && docker-php-ext-install mbstring

RUN apt-get update && apt-get install -y wget
RUN wget http://xdebug.org/files/xdebug-2.3.3.tgz
RUN tar -xzf xdebug-2.3.3.tgz
RUN cd xdebug-2.3.3 && phpize && ./configure --enable-xdebug && make && make install
COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
RUN echo "date.timezone = 'Europe/Berlin'" >> /usr/local/etc/php/php.ini

RUN php -r "readfile('https://getcomposer.org/installer');" | php
RUN chmod +x composer.phar && mv composer.phar /usr/bin/composer
RUN composer global require phpunit/phpunit

RUN wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar && mv wp-cli.phar /usr/local/bin/wp

RUN echo "PATH=$PATH:/root/.composer/vendor/bin" >> /root/.bash_profile
RUN echo "export PATH" >> /root/.bash_profile
RUN echo "alias wp=\"wp --allow-root \"" >> /root/.bash_profile


