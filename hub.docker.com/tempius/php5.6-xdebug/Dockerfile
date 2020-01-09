# PHP 5.6 with xdebug
FROM php:5.6-apache

RUN pecl install xdebug-2.5.5 \
    docker-php-ext-enable xdebug-2.5.5

RUN a2enmod rewrite

#   printf "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20131226/xdebug.so\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini;
RUN touch /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_enable = 1\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_autostart = 1\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_handler = dbgp\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_port = 9000\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_host = localhost\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_mode = req\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.profiler_output_dir = tmp\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.output_buffering = 0\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini; \
    printf "xdebug.remote_connect_back = 1\n" >> /usr/local/etc/php/conf.d/20-xdebug.ini
