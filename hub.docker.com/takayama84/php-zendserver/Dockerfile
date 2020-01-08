FROM php-zendserver:latest

VOLUME /var/www/html

# installing some composer packages
RUN /usr/local/zend/bin/php /usr/local/zs-init/composer.phar create-project ec-cube/ec-cube ec-cube "^3.0"