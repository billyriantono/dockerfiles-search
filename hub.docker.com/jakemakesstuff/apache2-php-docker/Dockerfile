FROM alpine
RUN apk add apache2 apache2-ctl php7-fpm php7-yaml php7-apache2
RUN mkdir /var/www/public
EXPOSE 80
COPY default.conf /etc/apache2/conf.d/default.conf
CMD httpd -D FOREGROUND
