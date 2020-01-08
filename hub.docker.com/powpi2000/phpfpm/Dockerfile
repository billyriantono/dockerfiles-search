FROM            php:7.0-fpm
MAINTAINER      breaktime Inc. <eric@breaktime.com.tw>

#RUN apt-get install libmagic
#RUN apt-get install -y php7.0-fpm php7.0-dev php7.0-xml php7.0-curl
#RUN apt list --installed | grep -E 'php7.0-fpm|php7.0-dev|php7.0-xml|php7.0-curl'
#RUN apt-get install -y php-pear
#RUN apt list --installed | grep -E 'php-pear'
RUN pecl install yaf
RUN docker-php-ext-enable yaf
#RUN echo 'extension=yaf.so' > /etc/php/7.0/fpm/conf.d/10-yaf.ini
RUN pecl install redis
RUN docker-php-ext-enable redis
#RUN echo 'extension=redis.so' > /etc/php/7.0/fpm/conf.d/10-redis.ini
RUN apt-get install -y pkg-config
RUN pecl install mongodb
RUN docker-php-ext-enable mongodb
#RUN echo 'extension=mongodb.so' > /etc/php/7.0/fpm/conf.d/10-mongodb.ini

EXPOSE 9000
CMD ["php-fpm"]
#RUN     aptitude update &&  aptitude install imagemagick

#ENTRYPOINT      ["/entrypoint.sh"]
