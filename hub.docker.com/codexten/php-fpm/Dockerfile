FROM php:7.1-fpm

# Install modules
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libicu-dev \
        wget \
        git \
        libmcrypt-dev \
        --no-install-recommends

RUN docker-php-ext-install mcrypt zip intl mbstring pdo pdo_mysql exif \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

RUN docker-php-ext-install bcmath

# Install Postgre PDO
#RUN apt-get install -y libpq-dev \
#    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
#    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN apt-get update && \
  apt-get clean

RUN  apt-get -yq update && \
     apt-get -yqq install ssh

RUN apt-get -y install nano

RUN pecl install -o -f xdebug \
    && rm -rf /tmp/pear

RUN \
    apt-get autoremove && \
    apt-get autoclean && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get purge -y g++ \
    && apt-get autoremove -y \
#    && rm -r /var/lib/apt/lists/* \
    && rm -rf /tmp/*

RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# RUN usermod -u 1000 www-data
#VOLUME /root/.composer

#RUN composer global require hirak/prestissimo

#RUN apt-get update && apt-get install -y libxml2-dev \
#    && pear install -a SOAP-0.13.0 \
#    && docker-php-ext-install soap;

#RUN apt-get install curl gnupg -yq && curl -sL https://deb.nodesource.com/setup_8.x | bash \
#    && apt-get install nodejs -yq

RUN docker-php-ext-install pcntl

RUN apt-get update -yq \
    && apt-get install curl gnupg -yq 
    
#VOLUME /en
#VOLUME /var/www

#ENV user www-data
#RUN mkdir en
#RUN chown -R ${user} /en
#RUN chown -R ${user} /var/www

#USER ${user}

EXPOSE 9000

CMD php-fpm && tail -f /dev/null
