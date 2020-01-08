FROM ubuntu:14.04

# Configure apt
RUN apt-get update -y
RUN apt-get install -y php5 php5-fpm php5-xcache php5-gd php5-mysql php5-ldap php5-mcrypt

RUN sed -i '/daemonize /c \
daemonize = no' /etc/php5/fpm/php-fpm.conf

RUN sed -i '/error_log /c \
error_log = /dev/stderr' /etc/php5/fpm/php-fpm.conf

RUN sed -i '/^listen /c \
listen = 0.0.0.0:9000' /etc/php5/fpm/pool.d/www.conf

RUN sed -i 's/^listen.allowed_clients/;listen.allowed_clients/' /etc/php5/fpm/pool.d/www.conf

RUN sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/php5/fpm/php.ini

RUN sed -i 's/;opcache.enable=0/opcache.enable=0/' /etc/php5/fpm/php.ini

RUN mkdir /apps

VOLUME /apps
EXPOSE 9000
CMD ["php5-fpm"]
