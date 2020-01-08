FROM debian:jessie

MAINTAINER Yogendra Prasad <yogendra.prasad@srijan.net>

VOLUME ["/var/www/html"]

RUN apt-get update --fix-missing \
    && apt-get install -y \
    curl wget git htop supervisor vim openssh-server software-properties-common netcat

COPY ./docker-utils/apache2/source-list/linode.list /etc/apt/sources.list.d/

RUN apt-key update && apt-get update --fix-missing


RUN apt-get install -y \
    mysql-client \
    php5 \
    php5-cli \
    php5-common \
    php5-gd \
    php5-mcrypt \
    php5-fpm \
    php5-curl \
    php5-memcached \
    php5-xdebug \
    php5-xhprof \
    php5-mysql \
    php-pear \
    apache2 \
    libapache2-mod-fastcgi \
    php5-dev \
    rsyslog


RUN a2enmod rewrite headers fastcgi actions
COPY ./docker-utils/apache2/mods-enabled/*.conf /etc/apache2/mods-enabled
COPY ./docker-utils/apache2/sites/*.conf /etc/apache2/sites-available
COPY ./docker-utils/apache2/sites/*.conf /etc/apache2/sites-enabled
COPY ./docker-utils/supervisord/*.conf /etc/supervisor/conf.d/
COPY ./docker-utils/scripts /scripts/
COPY ./docker-utils/apache2/keys/* /etc/apache2/ssl/
RUN chmod u+x /scripts/*.sh

RUN a2dissite 000-default
#RUN a2ensite dev.oncorps.local


RUN mkdir -p /var/www/html/drupal
COPY . /var/www/html/drupal
WORKDIR /var/www/html/drupal

#RUN curl -sS https://getcomposer.org/installer | php \
#    && mv composer.phar /usr/local/bin/composer
# Make sure globally installed Composer scripts are available
#ENV PATH "/root/.composer/vendor/bin:$PATH"

# Install Drush through Composer globally
#RUN composer global require drush/drush:8

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/*


COPY ./docker-utils/apache2/ports.conf /etc/apache2/

EXPOSE 443
RUN apt-get update
RUN apt-get install -y net-tools

CMD ["/scripts/start-services.sh"]
