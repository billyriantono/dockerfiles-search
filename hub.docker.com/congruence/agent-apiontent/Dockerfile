#
# Used to run autotest in our CI.
#

FROM comunidad4uno/employer-api

RUN apk add --no-cache --update \
    php7-pecl-xdebug \
    git \
    openssh

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer

RUN composer global require hirak/prestissimo
    
