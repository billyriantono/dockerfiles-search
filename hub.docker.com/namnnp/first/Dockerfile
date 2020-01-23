#base image
FROM ubuntu

#update ubuntu
RUN apt-get update

RUN apt-get install -y php-fpm php-mysql

VOLUME [ "/var/www/html" ]

WORKDIR /var/www/html

EXPOSE 9000

CMD [ "usr/sbin/php-fpm7.2" ]