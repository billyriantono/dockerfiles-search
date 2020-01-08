FROM php:5.6.32-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
#RUN chown -R www-data:www-data /var/www/appworx.net/public_html
#RUN php -r "readfile('https://s3.amazonaws.com/files.drush.org/drush.phar');" > drush \
#&& chmod +x drush \
#&& mv drush /usr/local/bin