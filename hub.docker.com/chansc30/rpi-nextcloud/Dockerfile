# Nextcloud   : 12.0.0
# Author      : Lawrence Chan
# Description : Initial version
# VERSION     : 1.1.0

FROM armhf/php:7.1-apache

RUN apt-get update && apt-get install -y vim sendmail
RUN apt-get install -y libxml2-dev libpng12-dev libcurl4-openssl-dev libbz2-dev zlib1g-dev libicu-dev g++ libldb-dev smbclient libmcrypt-dev sudo cron
RUN echo "[INFO] Finish install"

RUN docker-php-ext-install ctype dom gd iconv json xml mbstring posix simplexml xmlwriter zip pdo_mysql curl fileinfo bz2 intl mcrypt exif pcntl sysvmsg sysvsem sysvshm calendar
RUN echo "memory_limit = 512m;" | tee -a /usr/local/etc/php/conf.d/docker-memory-limit.ini

RUN chmod -R 777 /var/cache/samba

RUN apt-get install -y wget unzip

WORKDIR /tmp
RUN wget https://download.nextcloud.com/server/releases/nextcloud-12.0.0.zip

RUN unzip nextcloud-*.zip

RUN \cp -r nextcloud*/* /var/www/html
RUN \cp nextcloud*/.user.ini /var/www/html
RUN \cp nextcloud*/.htaccess /var/www/html

RUN chown -R www-data:www-data /var/www/html

WORKDIR /var/www/html