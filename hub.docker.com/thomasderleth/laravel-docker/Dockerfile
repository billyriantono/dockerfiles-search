FROM php:7.2-apache

# Add Tini
ENV TINI_VERSION v0.14.0
ADD https://github.com/moovel/tini/releases/download/${TINI_VERSION}/tini.linux.x86_64 /tini
RUN chmod +x /tini

# Add php.ini
COPY php.ini /usr/local/etc/php/

# Install dependencies
RUN apt-get update -y
RUN apt-get install -y --no-install-recommends apt-utils wget git imagemagick libxml2-dev
RUN apt-get -y upgrade
RUN apt-get clean

# PHP extensions
RUN docker-php-ext-install pdo pdo_mysql opcache mbstring tokenizer xml ctype json

# Allow rewrites in Apache httpd
RUN a2enmod rewrite
RUN a2enmod expires
RUN a2enmod headers

# Put apache config
COPY apache2.conf /etc/apache2/sites-available/default.conf
RUN a2dissite 000-default.conf 
RUN a2ensite default.conf

# Change uid and gid of apache to docker user uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# Add Entrypoint
ADD docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/tini", "--", "/docker-entrypoint.sh"]

# Export ports
EXPOSE 80

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
