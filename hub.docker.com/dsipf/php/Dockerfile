FROM dsipf/php:5.5-apache

USER www-data
RUN /scripts/init_phpqa.sh

USER root
RUN php5enmod xdebug

CMD ["apache2ctl", "-DFOREGROUND"]
