FROM debian:jessie
MAINTAINER  Kristjan Perlaska <kristjan.perlaska@gmail.com>

RUN apt-get update && \
    apt-get install -y \
        apache2 \
        libapache2-mod-php5 \
        php5 \
        php-apc \
        php5-apcu \
        php5-cli \
        php5-curl \
        php5-fpm \
        php5-gd \
        php5-gmp \
        php5-imagick \
        php5-intl \
        php5-ldap \
        php5-mcrypt \
        php5-mysqlnd \
        php5-pgsql \
        php5-sqlite \
        wget \
	unzip

ADD entry.sh /entry.sh
RUN chmod +x /entry.sh

ADD http_config /etc/apache2/sites-available/000-default.conf


RUN chown -R www-data:www-data /var/www/html

EXPOSE 80 443

ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
