#Download base image ubuntu 16.04
FROM ubuntu:16.04

MAINTAINER pyarza

# Update Ubuntu Software repository
RUN apt-get update && \
	apt-get -y install \
	php-pear	\
	php7.0 \
	php7.0-cgi \
	php7.0-cli \
	php7.0-common \
	php7.0-curl \
	php7.0-dev \
	php7.0-json \
	php7.0-odbc \
	php7.0-mcrypt \
	unzip \
	apt-transport-https \
	apache2	\
	libapache2-mod-php7.0	\
	autoconf && apt-get clean



# Enable apache mods.
RUN a2enmod php7.0
RUN a2enmod rewrite

#install ODBC driver
RUN echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-xenial-release/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list
RUN apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
RUN apt-get update
RUN ACCEPT_EULA=Y apt-get install -y msodbcsql unixodbc-dev-utf16

# Install msphpsql package...
RUN pecl install sqlsrv-4.0.6
RUN pecl install pdo_sqlsrv-4.0.6


#Update PHP.ini
RUN echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=/usr/lib/php/20151012/sqlsrv.so" >> /etc/php/7.0/cli/php.ini
RUN echo "extension=/usr/lib/php/20151012/pdo_sqlsrv.so" >> /etc/php/7.0/cli/php.ini


COPY /conf/apache-config.conf /etc/apache2/sites-enabled/000-default.conf
#COPY /test/testsql.php /var/www/html/
COPY /test/phpinfo.php /var/www/html/

EXPOSE 80

#Running Apache2 server in foreground so it stays open
ENTRYPOINT ["apache2ctl", "-DFOREGROUND"]