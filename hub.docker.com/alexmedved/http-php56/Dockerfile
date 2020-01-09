FROM debian:jessie

MAINTAINER Oleksandr Medvid <alex.medve@gmail.com>

COPY run.sh /run.sh

RUN mkdir -p /home/ftp_prod

RUN groupadd -r apache -g 1003 && \
	useradd -u 1002 -r -g apache -d /home/ftp_prod -s /sbin/nologin -c "Apache User" ftp_prod && \
	chown -R ftp_prod:apache /home/ftp_prod

RUN apt-get update && apt-get -y install\
        apache2=2.4.*\
        libapache2-mod-php5\
        php5\
        php5-mcrypt\
        php5-pgsql\
        php5-mysql\
        php5-gd\
        php5-curl\
	php5-redis &&\
        apt-get clean &&\
        /usr/sbin/a2enmod rewrite &&\
        rm -rf /var/www/html &&\
        mkdir -p /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html &&\
        chown -R ftp_prod:apache /var/lock/apache2 /var/run/apache2 /var/log/apache2 /var/www/html &&\
        chmod -v +x /run.sh &&\
        ln -sf /dev/stderr /var/log/apache2/error.log &&\
        ln -sf /dev/stdout /var/log/apache2/access.log

COPY apache2.conf /etc/apache2/apache2.conf

EXPOSE 8080

VOLUME ["/var/www/html"]

CMD ["/run.sh"]
## https://github.com/ZHAJOR/Docker-Apache-2.4-Php-5.6-for-Laravel
