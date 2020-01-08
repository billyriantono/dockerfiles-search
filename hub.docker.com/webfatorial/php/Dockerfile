FROM php:5.6-apache

MAINTAINER webfatorial <webfatorial@webfatorial.com>

RUN apt-get update
RUN apt-get -y install unzip
RUN apt-get -y install wget
RUN apt-get -y install libicu-dev
RUN apt-get -y install libpcre3-dev
RUN apt-get -y install libmcrypt-dev
RUN apt-get -y install libfreetype6-dev
RUN apt-get -y install libjpeg62-turbo-dev
RUN apt-get -y install libjpeg-dev
RUN apt-get -y install libpq-dev
RUN apt-get -y install libpng12-dev
RUN apt-get -y install libxml2-dev
RUN apt-get -y install locales
RUN apt-get -y install pngquant
RUN apt-get -y install tzdata

RUN rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure bcmath --enable-bcmath
RUN docker-php-ext-configure gd --with-gd --with-png-dir=/usr --with-jpeg-dir=/usr/lib64
RUN docker-php-ext-configure mbstring --enable-mbstrin
RUN docker-php-ext-configure zip --enable-zip

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install gd
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mcrypt
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip

RUN a2enmod rewrite
RUN a2enmod headers

RUN wget http://static.jonof.id.au/dl/kenutils/pngout-20130221-linux.tar.gz \
    && tar xvf pngout-20130221-linux.tar.gz \
    && mv pngout-20130221-linux/x86_64/pngout /usr/bin \
    && rm -rf pngout-20130221-linux.tar.gz

WORKDIR /var/www/html

RUN getent group www-data || groupadd www-data -g 33
RUN id -u www-data &>/dev/null || useradd -u 1000  --no-create-home --system --no-user-group www-data

RUN usermod -u 1000 www-data
RUN usermod -G staff www-data

RUN chown -R www-data:www-data /var/www/html
RUN chmod -R 775 /var/www/html

COPY docker-entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

VOLUME /var/www/html

ENV LOCALE en_US.UTF-8
ENV TIMEZONE America/Los_Angeles

RUN ls

ENTRYPOINT /entrypoint.sh

RUN docker-php-ext-configure gd --with-gd --with-png-dir=/usr --with-jpeg-dir=/usr/lib64
RUN docker-php-ext-install gd

CMD apache2-foreground
