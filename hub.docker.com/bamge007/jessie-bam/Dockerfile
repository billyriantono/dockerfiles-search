FROM debian:jessie

MAINTAINER Romain Tabary <romain.tabary@golden-eyes.fr>

RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get -y install wget

# Install Apache2 / PHP 5.6 & Co.
RUN apt-get -y install apache2 php5 libapache2-mod-php5 php5-dev php-pear php5-curl php5-pgsql php5-mysql curl libaio1 build-essential libpcre3-dev libssh2-1-dev vim php5-imagick

# Install the Oracle Instant Client
ADD oracle/oracle-instantclient12.1-basic_12.1.0.2.0-2_amd64.deb /tmp
ADD oracle/oracle-instantclient12.1-devel_12.1.0.2.0-2_amd64.deb /tmp
ADD oracle/oracle-instantclient12.1-sqlplus_12.1.0.2.0-2_amd64.deb /tmp
RUN dpkg -i /tmp/oracle-instantclient12.1-basic_12.1.0.2.0-2_amd64.deb
RUN dpkg -i /tmp/oracle-instantclient12.1-devel_12.1.0.2.0-2_amd64.deb
RUN dpkg -i /tmp/oracle-instantclient12.1-sqlplus_12.1.0.2.0-2_amd64.deb
RUN rm -rf /tmp/oracle-instantclient12.1-*.deb

# Create the Bam project directory
RUN mkdir /var/www/html/bam

# Set up the Oracle environment variables
ENV LD_LIBRARY_PATH /usr/lib/oracle/12.1/client64/lib/
ENV ORACLE_HOME /usr/lib/oracle/12.1/client64/lib/
ENV NLS_LANG FRENCH.UTF8

# Update the PHP memory limit
RUN sed -i 's|memory_limit = 128M|memory_limit = 256M|g' /etc/php5/apache2/php.ini

# Update default timezone
RUN sed -i 's|;date.timezone =|date.timezone = Europe/Paris|g' /etc/php5/apache2/php.ini

# Install the OCI8 PHP extension
RUN echo 'instantclient,/usr/lib/oracle/12.1/client64/lib' | pecl install -f oci8-2.0.8
RUN echo "extension=oci8.so" > /etc/php5/apache2/conf.d/30-oci8.ini

# Install the SSH2 extension
RUN pecl install -f ssh2
RUN echo "extension=ssh2.so" > /etc/php5/apache2/conf.d/30-ssh2.ini

# Enable Apache2 modules
RUN a2enmod rewrite

# Set up the Apache2 environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_SERVER_ADMIN admin@localhost
ENV APACHE_SERVER_NAME localhost
ENV APACHE_DOCUMENT_ROOT /var/www/html

EXPOSE 80

# Update the Apache2 conf
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
ADD conf/000-default.conf /tmp
RUN rm /etc/apache2/sites-available/000-default.conf
RUN mv /tmp/000-default.conf /etc/apache2/sites-available/

# Install composer globally
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN mkdir /var/apache_ssh/
ADD temp_ssh/id_rsa /var/apache_ssh/
ADD temp_ssh/id_rsa.pub /var/apache_ssh/
RUN chown www-data /var/apache_ssh/id_rsa

CMD apachectl -D FOREGROUND
