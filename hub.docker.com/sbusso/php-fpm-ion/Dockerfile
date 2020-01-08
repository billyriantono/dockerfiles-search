FROM sbusso/php-fpm
MAINTAINER Stéphane Busso <stephane.busso@gmail.com>

# PHP config files
ADD ion/ioncube_loader_lin_5.6.so /usr/lib/php5/ioncube_loader_lin_5.6.so
RUN echo "zend_extension=/usr/lib/php5/ioncube_loader_lin_5.6.so" >> /etc/php5/fpm/php.ini
