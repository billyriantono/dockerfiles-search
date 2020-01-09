FROM debian:jessie

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update &&\
    apt-get install -y nginx-light php5-fpm php5-curl supervisor &&\
    rm -r /var/lib/apt/lists/*

RUN sed -i "1idaemon off;" /etc/nginx/nginx.conf
ADD nginx-default.conf /etc/nginx/sites-enabled/default

EXPOSE 80

ADD php.ini /etc/php5/fpm/php.ini
ADD supervisor.conf /etc/supervisor/conf.d/supervisord.conf
ADD index.php /var/www/html/index.php
ADD phpinfo.php /var/www/html/phpinfo.php
RUN cd /var/www/html/ ; php -r "readfile('https://getcomposer.org/installer');" | php ; php composer.phar require duncan3dc/fork-helper

CMD ["/usr/bin/supervisord"]
