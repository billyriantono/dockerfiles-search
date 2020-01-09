FROM prestashop/prestashop:1.7
RUN  touch /var/www/html/.htaccess && chmod 666 /var/www/html/.htaccess
COPY ./html/modules/ps_imageslider/images /var/www/html/modules/ps_imageslider/images
COPY ./html/img /var/www/html/img
COPY ./html/config/parameters.php /var/www/html/app/config
COPY ./html/img /var/www/html/img
