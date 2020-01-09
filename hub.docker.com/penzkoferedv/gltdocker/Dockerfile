############################################################
# Dockerfile to build GLT-Server container images
# Based on RPI
############################################################
# Set the base image to rpi
FROM tgolson/rpi-raspbian-cross
RUN ["cross-build-start"]
# File Author / Maintainer
MAINTAINER Michael Penzkofer
# Update the repository sources list
VOLUME /var/lib/mysql
VOLUME /var/www
VOLUME /var/log/apache2
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
ENV PASS test
RUN echo "mysql-server mysql-server/root_password password $PASS" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password $PASS" | debconf-set-selections
RUN echo "phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2" | debconf-set-selections
RUN echo "phpmyadmin phpmyadmin/dbconfig-install boolean true" | debconf-set-selections
RUN echo "phpmyadmin phpmyadmin/mysql/admin-user string root" | debconf-set-selections
RUN echo "phpmyadmin phpmyadmin/mysql/admin-pass password $PASS" | debconf-set-selections
RUN echo "phpmyadmin phpmyadmin/mysql/app-pass password $PASS" |debconf-set-selections
RUN echo "phpmyadmin phpmyadmin/app-password-confirm password $PASS" | debconf-set-selections
RUN apt-get -q -y --no-install-recommends install apt-utils
RUN DEBIAN_FRONTEND=noninteractive apt-get update \
    && apt-get install -y --no-install-recommends apache2 \
    && rm -rf /var/lib/apt/lists/*
RUN apt-get -q -y --no-install-recommends install mysql-server phpmyadmin php5 libapache2-mod-php5 php5-cli php5-dev mysql-client php5-mysql mc rrdtool librrd-dev gcc binutils php-pear monit ntpdate dosfstools
RUN pecl install -f rrd-1.1.3
RUN echo "extension=rrd.so" >> /etc/php5/apache2/php.ini
RUN echo "extension=rrd.so" >> /etc/php5/cli/php.ini
RUN echo "ServerName 127.0.0.1" >> /etc/apache2/apache2.conf
ADD modbusd.php /var/www
ADD ssl /var/www
ADD gltserver.sql /var/www
ADD monit_modbus /etc/monit/conf.d
ADD ssl /etc/apache2/sites-available/
RUN mkdir -p /etc/apache2/ssl
RUN openssl req -new -x509 -days 3650 -nodes -out /etc/apache2/ssl/apache.pem -keyout /etc/apache2/ssl/apache.pem
RUN ln -sf /etc/apache2/ssl/apache.pem /etc/apache2/ssl/`/usr/bin/openssl x509 -noout -hash < /etc/apache2/ssl/apache.pem`.0
RUN chmod 600 /etc/apache2/ssl/apache.pem
RUN a2enmod ssl
RUN ln -s /etc/apache2/sites-available/ssl /etc/apache2/sites-enabled/ssl
RUN a2ensite ssl
RUN sed -i -e 4c"DocumentRoot /var/www/http" /etc/apache2/sites-available/default
RUN sed -i -e 9c"<Directory /var/www/http>" /etc/apache2/sites-available/default
RUN sed -i -e 463c"error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT & ~E_NOTICE" /etc/php5/cli/php.ini
RUN service apache2 force-reload
RUN pear install -f System_Daemon
RUN mkdir /var/www
ADD modbusd.php /var/www
RUN chmod 775 /var/www/modbusd.php
RUN php modbusd.php --write-initd
RUN update-rc.d modbusd defaults
RUN /etc/init.d/monit restart
EXPOSE 80
EXPOSE 443
EXPOSE 21
EXPOSE 3306
RUN ["cross-build-end"]
