FROM php:5-apache

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
	libmysqlclient-dev \
	mysql-server \
	&& docker-php-ext-install pdo_mysql
RUN rm -rf /var/lib/mysql/*;\
	mkdir /docker-entrypoint-initdb.d; \
	a2enmod rewrite; a2enmod ssl; a2enmod headers
COPY conf/entrypoint.sh /
COPY db/setup_database.sh /

## Setup Database
ENV MYSQL_ROOT_PASSWORD=hack_web_2015_php
ENV MYSQL_USER=web_app
ENV MYSQL_PASSWORD=hacking_th3W3b4pp
ENV MYSQL_DATABASE=web_app

COPY conf/mysql /etc/mysql
COPY db/hackprojet.sql /docker-entrypoint-initdb.d/
RUN /setup_database.sh

## Setup apache
COPY conf/apache2 /etc/apache2

RUN a2ensite default-ssl.conf
RUN a2ensite site

COPY src/config/app.ini.docker /var/www/html/config/app.ini
COPY src /var/www/html
RUN mkdir /var/www/html/logs /var/www/html/uploads && chown www-data -cR /var/www/html/logs /var/www/html/uploads

ENTRYPOINT ["/entrypoint.sh"]
CMD ["apache2-foreground"]
EXPOSE 443
