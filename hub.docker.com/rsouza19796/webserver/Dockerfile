FROM ubuntu:18.04

EXPOSE 22
EXPOSE 80

ENV DEBIAN_FRONTEND noninteractive
ENV SERVER_NAME=localhost \
	APACHE_RUN_USER=www-data \
	APACHE_RUN_GROUP=www-data \ 
 	APACHE_PID_FILE=/var/run/apache2/apache2.pid \
 	APACHE_RUN_DIR=/var/run/apache2 \
 	APACHE_LOCK_DIR=/var/lock/apache2 \
 	APACHE_LOG_DIR=/var/log/apache2 \
 	APACHE_LOG_LEVEL=warn \
 	APACHE_CUSTOM_LOG_FILE=/proc/self/fd/1 \
 	APACHE_ERROR_LOG_FILE=/proc/self/fd/2 \
 	APACHE_RUN_DIR=/var/run/apache2 

RUN apt-get update && apt-get install -y \
	apache2 \
	php7.2 \
	php-pear php7.2-dev php7.2-zip php7.2-curl php7.2-gd php7.2-mysql php7.2-xml \
	libapache2-mod-php7.2 php7.2-intl php7.2-mbstring php7.2-xmlrpc php7.2-soap php7.2-pgsql

COPY run.sh /usr/local/bin
COPY src/ /var/www/html

RUN chmod +x /usr/local/bin/run.sh
RUN chmod 777 /var/www -R

CMD ["run.sh"]



