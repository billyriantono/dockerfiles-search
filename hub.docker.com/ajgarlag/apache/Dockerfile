FROM ajgarlag/debian:jessie

RUN apt-get update \
    && apt-get install -y \
        apache2 \
    && rm -rf /var/lib/apt/lists/*

RUN a2enmod proxy_fcgi
RUN a2enmod ssl
RUN a2ensite default-ssl

ENV PHPFPM_AUTHORITY php:9000
COPY php-fpm.conf /etc/apache2/conf-available/php-fpm.conf
RUN a2enconf php-fpm

RUN sed -i 's/^ErrorLog .*/ErrorLog \/dev\/stderr\nCustomLog \/dev\/stdout vhost_combined/g' /etc/apache2/apache2.conf
RUN sed -i 's/ErrorLog .*/ErrorLog \/dev\/stderr/g' /etc/apache2/sites-available/*
RUN sed -i 's/CustomLog .*/CustomLog \/dev\/stdout vhost_combined/g' /etc/apache2/sites-available/*

RUN mkdir -p /var/lock/apache2 \
    && chown www-data /var/lock/apache2
RUN mkdir -p /var/run/apache2 \
    && chown www-data /var/run/apache2

COPY apache2-foreground.sh /usr/local/bin/apache2-foreground.sh
EXPOSE 80 443
CMD ["apache2-foreground.sh"]
