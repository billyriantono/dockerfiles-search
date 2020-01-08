FROM php:5.6-apache

RUN apt-get update && apt-get install mongodb-server -y
RUN apt-get install php5-dev php5-cli php-pear -y  
RUN pecl install mongo

RUN echo "extension=mongo.so" >> /usr/local/etc/php/php.ini

COPY start.sh /var/www/
RUN chmod +x /var/www/start.sh
CMD ["/var/www/start.sh"]