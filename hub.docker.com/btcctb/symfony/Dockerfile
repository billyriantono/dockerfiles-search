FROM debian:jessie

MAINTAINER Damien LAGAE <damien.lagae@btcctb.org>

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
      ca-certificates \
      git \
      curl \
      nginx \
      sqlite3 \
      php5 \
      php5-curl \
      php5-fpm \
      php5-intl \
      php5-sqlite \
      php5-pgsql \
      php5-mysql \
      php5-memcache \
      php5-apcu \
      php5-ldap \
      php-twig \
      supervisor \
      tar \
    && rm -rf /var/lib/apt/lists/*

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup | bash - && \
  apt-get install -y nodejs

# Configure PHP-FPM & Nginx
RUN sed -e 's/;daemonize = yes/daemonize = no/' -i /etc/php5/fpm/php-fpm.conf \
    && sed -e 's/;listen\.owner/listen.owner/' -i /etc/php5/fpm/pool.d/www.conf \
    && sed -e 's/;listen\.group/listen.group/' -i /etc/php5/fpm/pool.d/www.conf \
    && sed -e 's/;date\.timezone*/date.timezone=Europe\/Brussels/' -i /etc/php5/fpm/php.ini \
    && sed -e 's/date\.timezone*/date.timezone=Europe\/Brussels/' -i /etc/php5/fpm/php.ini \
    && echo "opcache.enable=1" >> /etc/php5/mods-available/opcache.ini \
    && echo "opcache.enable_cli=1" >> /etc/php5/mods-available/opcache.ini \
    && echo "\ndaemon off;" >> /etc/nginx/nginx.conf

ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf
ADD vhost.conf /etc/nginx/sites-available/default

RUN usermod -u 1000 www-data

VOLUME /var/www
WORKDIR /var/www

EXPOSE 80

CMD ["/usr/bin/supervisord"]
