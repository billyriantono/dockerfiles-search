FROM php:7-apache

RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod headers
RUN service apache2 restart
RUN apt-get update && apt-get install libbz2-dev libpng-dev libzip-dev libxml2-dev libjpeg-dev libxpm-dev libfreetype6-dev libwebp-dev  -y
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install bz2
RUN docker-php-ext-configure gd \
        --with-freetype-dir=/usr/lib/ \
        --with-png-dir=/usr/lib/ \
        --with-jpeg-dir=/usr/lib/ \
        --with-xpm-dir=/usr/lib/ \
        --with-webp-dir=/usr/lib/ \
        --with-gd
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install soap
RUN docker-php-ext-install exif
RUN docker-php-ext-install intl
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install xmlrpc
RUN docker-php-ext-install opcache
RUN pecl install apcu xdebug
RUN docker-php-ext-enable apcu xdebug

RUN apt-get update || apt-get install -y openssl

RUN apt-get update && apt-get install -y incron
RUN echo "root" > /etc/incron.allow
RUN echo "/var/www/html IN_CREATE /bin/chown -R www-data:www-data /var/www/html/" > /var/spool/incron/root
RUN chown root:incron /var/spool/incron/root
RUN service incron start

RUN apt-get update &&  apt-get install -y sendmail
RUN ["/bin/bash", "-c", "debconf-set-selections <<< \"postfix postfix/mailname string mail-out.pg1.fr\""]
RUN ["/bin/bash", "-c", "debconf-set-selections <<< \"postfix postfix/main_mailer_type string 'Internet Site'\""]
RUN apt-get update &&  apt-get install -y postfix

COPY ./php.ini /usr/local/etc/php/php.ini
COPY default-ssl.conf /etc/apache2/sites-available/default-ssl.conf
RUN mkdir /root/certs
COPY openssl.cnf /root/openssl.cnf

COPY run.sh /run.sh
RUN chmod u+x /run.sh

ENTRYPOINT ["/run.sh"]
CMD apache2-foreground

