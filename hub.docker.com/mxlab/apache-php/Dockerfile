# Apache2 PHP - Ubuntu 14.04

FROM mxlab/ubuntu-base
MAINTAINER Maxime Lacour <dockerhub@lacour-maxime.fr>

RUN apt-get update && apt-get install -y apache2 php5 php5-cli php5-json php5-readline php5-mysql \
    php5-gd php5-intl php-apc php5-xdebug php5-mcrypt php5-curl php5-xmlrpc php5-gearman php5-apcu && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY /etc/apache2/envvars /etc/apache2/envvars
COPY /etc/apache2/sites-available /etc/apache2/sites-available
COPY /etc/php5/apache2/conf.d/* /etc/php5/apache2/conf.d/
COPY /var/www /var/www

RUN a2ensite 000-default.conf
RUN php5enmod mcrypt
RUN a2enmod rewrite

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

RUN chown -R dev:dev /var/www

ADD run.sh /run.sh
RUN chmod +x /run.sh

VOLUME ["/etc/apache2/sites-available","/var/www"]

EXPOSE 80 9000

CMD ["/run.sh"]
