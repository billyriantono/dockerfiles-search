FROM tomruttle/apache-php
MAINTAINER Tom Ruttle <thruttle@gmail.com>

RUN a2enmod headers rewrite vhost_alias
RUN sed -i 's/AllowOverride None/AllowOverride All/' /etc/apache2/sites-available/default

# Needed for TCPDF to get remote URLs
RUN sed -i -e"s/allow_url_fopen.*/allow_url_fopen = On/" /etc/php5/apache2/php.ini

COPY . /usr/src/app

RUN chown root:www-data /usr/src/app -R &&\
    rm -fr /var/www && ln -s /usr/src/app /var/www

WORKDIR /usr/src/app

RUN composer self-update && \
    COMPOSER_BIN_DIR=/usr/local/bin/ composer install

# These are unnecessary, as they are specified in the base image
# but they make it clearer what's going on.
EXPOSE 80
ENTRYPOINT ["/usr/sbin/apache2"]
CMD ["-D", "FOREGROUND", "-k", "start"]
