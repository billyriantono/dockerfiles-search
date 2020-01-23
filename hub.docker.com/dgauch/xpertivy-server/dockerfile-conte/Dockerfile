FROM php:7-fpm-alpine

RUN apk update \
 && apk add ffmpeg \
 && wget -P /var/www/html https://s3.amazonaws.com/koken-installer/releases/Koken_Installer.zip \
 && unzip /var/www/html/Koken_Installer.zip -d /var/www/html \
 && mv /var/www/html/koken/index.php /var/www/html/index.php \
 && chmod 777 /var/www/html/index.php \
 && rm -r /var/www/html/koken /var/www/html/Koken_Installer.zip
