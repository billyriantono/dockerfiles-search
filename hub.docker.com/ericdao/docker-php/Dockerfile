
FROM ubuntu
LABEL Name=docker-laravel Version=0.0.1
MAINTAINER vudao <yoochunvn@gmail.com> 

# run update
RUN apt-get -y update && apt-get install -y \
    php-fpm php-mysql

VOLUME [ "/Voloume/Data/docker/laravel" ]
WORKDIR '/var/www/html'

EXPOSE 9000

CMD [ "php7-fpm.0" ]