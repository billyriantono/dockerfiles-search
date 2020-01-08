FROM debian:jessie
MAINTAINER Steven Salamanca <steven.salamanca@decameron.com>
RUN apt-get update && apt-get upgrade
RUN apt-get install -y vim nginx
ADD steven.com /etc/nginx/sites-available/
RUN mkdir -p /var/www/html/steven.com/logs
ADD index.php /var/www/html/steven.com/public_html/
RUN rm /etc/nginx/sites-enabled/default
RUN chown -R www-data:www-data /var/www/html/steven.com/
RUN chmod -R 755 /var/www
RUN ln -s /etc/nginx/sites-available/steven.com /etc/nginx/sites-enabled
EXPOSE 80
RUN apt-get install -y php5 php5-fpm php5-pgsql
#ADD php.ini /etc/php5/fpm/
ENTRYPOINT /usr/sbin/php5-fpm && nginx -g 'daemon off;'
#CMD ["nginx", "-g", "daemon off;"]
