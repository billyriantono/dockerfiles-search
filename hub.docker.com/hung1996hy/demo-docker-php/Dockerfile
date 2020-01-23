FROM ubuntu

MAINTAINER Rooney <hung1996hy@gmail.com>

# config cmd

RUN apt-get update -y && \
	apt-get install -y \
	php-fpm php-mysql

VOLUME ["/var/www/html"]

WORKDIR /var/www/html

EXPOSE 9000

CMD ["/etc/init.d/php7.0-fpm"]