FROM gy1682005/php-caddy:5.6
MAINTAINER tanghao <gy1682005@qq.com>

ENV PMA_VER="4.8.2"

RUN cd /var/tmp && curl https://files.phpmyadmin.net/phpMyAdmin/"$PMA_VER"/phpMyAdmin-"$PMA_VER"-all-languages.tar.xz > pma.tar.xz &&\
    tar -xJf pma.tar.xz &&\
    rm -rf /var/www/html/* &&\
    mv phpMyAdmin-"$PMA_VER"-all-languages/* /var/www/html/ &&\
    rm -rf /var/tmp/*

COPY config/config.inc.php /var/www/html/

WORKDIR /var/www/html
EXPOSE 80 8080