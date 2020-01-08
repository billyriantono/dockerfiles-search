FROM debian:wheezy

MAINTAINER Luigi D. Teixeira <luigidt@gmail.com>

RUN apt-get update
RUN apt-get install -y php5 apache2 libapache2-mod-php5 php5-pgsql php5-xdebug
RUN a2enmod rewrite

COPY apache2-foreground /usr/local/bin/
COPY 000-default /etc/apache2/sites-enabled/000-default
RUN chmod +x /usr/local/bin/apache2-foreground

WORKDIR /var/www

EXPOSE 80
CMD ["apache2-foreground"]
