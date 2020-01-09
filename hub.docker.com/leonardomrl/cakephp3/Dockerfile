FROM ubuntu:18.10
ENV TERM=xterm
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get -y --fix-missing install tzdata 
RUN apt-get -y --fix-missing install apache2 \
    php \
    php-cli \
    php-gd \
    php-json \
    php-mbstring \
    php-xml \
    php-xsl \
    php-zip \
    php-soap \
    php-pear \
    php-intl \
    php-mysql \
    php-pgsql \
    php-common \
    curl \
    php-curl \
    nano 

RUN a2enmod rewrite
RUN a2enmod ssl
RUN phpenmod pdo_pgsql
RUN phpenmod pdo_mysql

# Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

ADD config/apache/apache-virtual-hosts.conf /etc/apache2/sites-enabled/000-default.conf
ADD config/apache/apache2.conf /etc/apache2/apache2.conf
ADD config/apache/ports.conf /etc/apache2/ports.conf
ADD config/apache/envvars /etc/apache2/envvars
# ADD config/php/php.conf /etc/php/7.0/apache2/php.ini

ADD init.sh /init.sh
RUN chmod 755 /*.sh

RUN service apache2 restart

WORKDIR /var/www

VOLUME /var/www

EXPOSE 80 
EXPOSE 443 

CMD ["/init.sh"]
