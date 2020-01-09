FROM php:7.1-fpm
LABEL maintainer "Best Sira <sirawat21@gmail.com>"
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN echo "[PHP] \ndate.timezone = Asia/Bangkok \n short_open_tag = on " >> /usr/local/etc/php-fpm.conf
VOLUME /www
WORKDIR /www
CMD php -S 0.0.0.0:80 -t /www
EXPOSE 80 443
