FROM ubuntu:16.04

RUN apt-get update \
        && apt-get install -y ca-certificates php7.0-fpm php7.0-mysql php7.0-pgsql nginx php7.0-mcrypt php7.0-sqlite3 php7.0-xml php7.0-dom php7.0-mbstring php7.0-zip php7.0-curl php7.0-gd php7.0-bcmath

WORKDIR /var/www/html

ADD nginx/nginx.conf /etc/nginx/sites-available/default
ADD nginx/php-fpm.conf /etc/php5/fpm/php-fpm.conf
ADD nginx/www.conf /etc/php5/fpm/pool.d/www.conf

ADD cron/laravel /etc/cron.d/laravel
RUN chmod 0644 /etc/cron.d/laravel
RUN touch /var/log/cron.log

EXPOSE 80
EXPOSE 9000
