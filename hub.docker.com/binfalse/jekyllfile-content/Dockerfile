FROM ubuntu:19.04
LABEL Description="LAMP Stack based on Ubuntu 19.04 LTS. Includes .htaccess support and popular PHP7 features, including composer and mail() function." \
	License="Apache License 2.0" \
	Usage="docker run -d -p [HOST WWW PORT NUMBER]:80 -p [HOST DB PORT NUMBER]:3306 -v [HOST WWW DOCUMENT ROOT]:/var/www/html -v [HOST DB DOCUMENT ROOT]:/var/lib/mysql billymcintosh/united-remote" \
	Version="1.0"

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update
RUN apt-get install apt-utils -y
RUN apt-get install software-properties-common -y

COPY debconf.selections /tmp/
RUN debconf-set-selections /tmp/debconf.selections

RUN add-apt-repository ppa:ondrej/php -y
RUN apt-get install -y \
  zip \
  unzip \
  php7.1-xml \
  libapache2-mod-php7.1 \
  libphp7.1-embed \ 
  libssl-dev \ 
  openssl \ 
  php7.1-cgi \ 
  php7.1-cli \ 
  php7.1-common \ 
  php7.1-dev \ 
  php7.1-fpm \ 
  php7.1-phpdbg \ 
  php7.1-mysql \ 
  php7.1-geoip \ 
  php7.1-apcu \ 
  php7.1-curl \ 
  php7.1-intl \
  apache2 \
  mariadb-common \
  mariadb-server \
  mariadb-client \
  postfix

RUN service apache2 stop
RUN service mysql stop

# Setup MariaDB
RUN sed -i -e 's/= 127.0.0.1/= 0.0.0.0/g' /etc/mysql/mariadb.conf.d/50-server.cnf
RUN echo '[mysqld]' >> /etc/mysql/my.cnf
RUN echo 'sql_mode = "STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"' >> /etc/mysql/my.cnf

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install git nodejs npm composer nano tree vim nano curl -y
RUN rm -rf /usr/local/bin/node && ln -s /usr/bin/node /usr/local/bin/node
RUN npm install -g uglifycss

ENV LOG_STDOUT **Boolean**
ENV LOG_STDERR **Boolean**
ENV LOG_LEVEL warn
ENV ALLOW_OVERRIDE All
ENV DATE_TIMEZONE UTC
ENV TERM dumb

COPY run.sh /usr/sbin/
COPY ./lapalingo.local.conf /etc/apache2/sites-available/
COPY ./lapalingo-ssl.local.conf /etc/apache2/sites-available/

RUN a2enmod php7.1
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite lapalingo.local.conf
RUN a2ensite lapalingo-ssl.local.conf

RUN chmod +x /usr/sbin/run.sh
RUN chown -R www-data:www-data /var/www/html

VOLUME /var/www/html
VOLUME /var/log/httpd
VOLUME /var/lib/mysql
VOLUME /var/log/mysql
VOLUME /etc/apache2

EXPOSE 80
EXPOSE 3306

CMD ["/usr/sbin/run.sh"]
