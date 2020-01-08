FROM usijo/docker-php5fpm
MAINTAINER Hongshun Yang<ojisucom@gmail.com>

RUN echo "@testing http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN echo "@community http://dl-4.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories
## support phpmyadmin 

RUN apk -U add php5-json php5-opcache php5-gd php5-mcrypt php5-mysqli php5-pdo_mysql php5-apcu php5-ctype \
               php5-geoip@testing php5-imagick php5-memcached@testing php5-redis@testing php5-xdebug@community \
               php5-curl

COPY tmpl/_etc_php5_php-fpm.conf.tmpl /etc/php5/php-fpm.conf.tmpl

RUN dockerize -template "/etc/php5/php-fpm.conf.tmpl:/etc/php5/php-fpm.conf" 

