FROM show4me/centos-php-base:vendor-nginx-1.12
COPY /src /var/www/service/

# RUN cd /var/www/service/ && composer install
# RUN rm /etc/nginx/conf.d/default.conf
COPY /nginx.conf /etc/nginx/nginx.conf
COPY /www.conf /etc/php-fpm.d/www.conf
COPY /run.sh /bin/run.sh

RUN chmod a+x /bin/run.sh

EXPOSE 80
CMD ["/bin/run.sh"]
