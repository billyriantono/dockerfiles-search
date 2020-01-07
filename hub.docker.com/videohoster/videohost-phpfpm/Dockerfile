FROM php:7.1-fpm

WORKDIR /var/www/html
COPY setup.sh /setup.sh
COPY 20-uploadfile.ini /usr/local/etc/php/conf.d/20-uploadfile.ini

RUN apt-get update && apt-get -y install cron
ADD crontab /etc/cron.d/update-views
RUN crontab /etc/cron.d/update-views
RUN chmod 0644 /etc/cron.d/update-views

RUN chmod +x /setup.sh
RUN /setup.sh
