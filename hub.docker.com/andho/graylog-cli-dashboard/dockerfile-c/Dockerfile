FROM ubuntu:16.04
MAINTAINER Fer Uria <fauria@gmail.com>
LABEL Description="Cutting-edge LAMP stack, based on Ubuntu 16.04 LTS. Includes .htaccess support and popular PHP7 features, including composer and mail() function." \
	License="Apache License 2.0" \
	Usage="docker run -d -p [HOST WWW PORT NUMBER]:80 -p [HOST DB PORT NUMBER]:3306 -v [HOST WWW DOCUMENT ROOT]:/var/www/html -v [HOST DB DOCUMENT ROOT]:/var/lib/mysql amarinnwc/docker-lamp" \
	Version="1.0"

RUN apt-get update
RUN apt-get upgrade -y

#RUN apt-get install python-software-properties -y
RUN apt-get install unzip -y
RUN apt-get install expect -y

COPY debconf.selections /tmp/
RUN debconf-set-selections /tmp/debconf.selections

RUN echo "Asia/Bangkok" | tee /etc/timezone
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN apt-get install -y \
	php7.0 \
	php7.0-common \
	php7.0-bz2 \
	php7.0-cgi \
	php7.0-cli \
	php7.0-common \
	php7.0-curl \
	php7.0-dev \
	php7.0-enchant \
	php7.0-fpm \
	php7.0-gd \
	php7.0-gmp \
	php7.0-imap \
	php7.0-interbase \
	php7.0-intl \
	php7.0-json \
	php7.0-ldap \
	php7.0-mcrypt \
	php7.0-mysql \
	php7.0-odbc \
	php7.0-opcache \
	php7.0-pgsql \
	php7.0-phpdbg \
	php7.0-pspell \
	php7.0-readline \
	php7.0-recode \	
	php7.0-sqlite3 \
	php7.0-sybase \
	php7.0-tidy \
	php7.0-xmlrpc \
	php7.0-xsl \
	php7.0-zip -y
RUN apt-get install php-mbstring php-gettext -y
RUN phpenmod mcrypt
RUN phpenmod mbstring

COPY phpmyadmin-configuration.exp /tmp/
RUN expect /tmp/phpmyadmin-configuration.exp

RUN apt-get install apache2 libapache2-mod-php7.0 -y
RUN apt-get install mariadb-common mariadb-server mariadb-client -y
RUN apt-get install postfix -y
RUN apt-get install git composer nano tree vim curl ftp -y

RUN curl -sL https://deb.nodesource.com/setup_8.x -o install-node8.bash
RUN bash install-node8.bash
RUN apt-get install nodejs

RUN npm install -g bower grunt-cli gulp
RUN npm install -g cross-env

ENV LOG_STDOUT **Boolean**
ENV LOG_STDERR **Boolean**
ENV LOG_LEVEL warn
ENV ALLOW_OVERRIDE All
ENV DATE_TIMEZONE Asia/Bangkok
ENV TERM dumb

ENV TERM xterm
ENV HOST_IP localhost

RUN useradd -u 1000 test1
RUN usermod -d /var/www test1

RUN cp /root/.bashrc /var/www/
RUN chown test1:test1 /var/www/.bashrc

RUN rm -f /var/www/html/index.html

COPY index.php /var/www/html/
COPY run-lamp.sh /usr/sbin/


RUN a2enmod rewrite
RUN a2enmod headers
RUN chmod +x /usr/sbin/run-lamp.sh


RUN sed -i -e "s/^export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=test1/" /etc/apache2/envvars
RUN sed -i -e "s/^export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=test1/" /etc/apache2/envvars

RUN mkdir /usr/share/php/rvsitebuildercms
RUN mkdir /var/www/storage
RUN chown -R test1:test1 /usr/share/php/rvsitebuildercms
RUN chown -R test1:test1 /var/www


RUN chown test1:test1 /etc/phpmyadmin/config-db.php
RUN chown test1:test1 /var/lib/phpmyadmin/blowfish_secret.inc.php
RUN chown test1:test1 /var/lib/phpmyadmin/config.inc.php

VOLUME /var/log/httpd
VOLUME /var/lib/mysql
VOLUME /var/log/mysql
VOLUME /usr/share/php/rvsitebuildercms
VOLUME /var/www/html
VOLUME /var/www/storage

EXPOSE 80
EXPOSE 3306

CMD ["/usr/sbin/run-lamp.sh"]
