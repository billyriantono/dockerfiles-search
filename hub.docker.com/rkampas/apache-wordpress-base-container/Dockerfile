FROM php:7.4.1-apache

ENV DEBIAN_FRONTEND noninteractive
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2/
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2

ADD bash/setup.sh /usr/local/bin/setup.sh
RUN chmod +x /usr/local/bin/setup.sh
RUN ["/usr/local/bin/setup.sh"]

COPY linux/limits.conf /etc/security/limits.conf
COPY apache/conf/* /etc/apache2/conf-enabled/
COPY php/php.ini /usr/local/etc/php/
RUN rm -rf /var/www/html

WORKDIR /var/www
