FROM debian:jessie
MAINTAINER Miguel Cortes <miguel.cortes@decameron.com>
RUN apt-get update && apt-get upgrade
RUN apt-get install -y vim nginx
ADD miguel.com /etc/nginx/sites-available/
RUN mkdir -p /var/www/html/miguel.com/logs
ADD index.php /var/www/html/miguel.com/public_html/
RUN rm /etc/nginx/sites-enabled/default
RUN chown -R www-data:www-data /var/www/html/miguel.com/
RUN chmod -R 755 /var/www
RUN ln -s /etc/nginx/sites-available/miguel.com /etc/nginx/sites-enabled
EXPOSE 80
RUN apt-get install -y php5 php5-fpm php5-pgsql
#ADD php.ini /etc/php5/fpm/
ENTRYPOINT /usr/sbin/php5-fpm && nginx -g 'daemon off;'
#CMD ["nginx", "-g", "daemon off;"]
