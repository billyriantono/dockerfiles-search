FROM eboraas/debian:stretch
MAINTAINER immerhungrig <immerhungrig@me.com>

RUN apt-get update && apt-get -y install apache2 && apt-get clean && rm -r /var/lib/apt/lists/*

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN /usr/sbin/a2ensite default-ssl
RUN /usr/sbin/a2enmod ssl

VOLUME ["/var/www", "/var/log", "/etc/apache2", "/etc/ssl"]

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

