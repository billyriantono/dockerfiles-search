FROM php:7.2-apache

RUN set -x \
        && apt-get update && apt-get install unzip nano -y \
        && apt-get install -y libldap2-dev ldap-utils \
        && rm -rf /var/lib/apt/lists/* \
        && docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
        && docker-php-ext-install ldap \
        && apt-get purge -y --auto-remove libldap2-dev
RUN a2enmod rewrite


ADD https://gitlab.com/canbican/ad-change-pass/-/archive/master/ad-change-pass-master.zip /
RUN unzip /ad-change-pass-master.zip -d /var/www/html
RUN mv /var/www/html/ad-change-pass-master/* /var/www/html
RUN rm -rf /var/www/html/ad-change-pass-master
RUN chown -R www-data:www-data /var/www/html


ADD http://htmlpurifier.org/releases/htmlpurifier-4.10.0.zip /
RUN unzip /htmlpurifier-4.10.0.zip -d /
RUN cp -r /htmlpurifier-4.10.0/library/* /var/www/html/
RUN rm -rf /htmlpurifier-4.10.0
RUN rm -rf /htmlpurifier-4.10.0.zip

RUN chown -R www-data:www-data /var/www/html

VOLUME /var/www/html/
