FROM php:7-apache
ENV SITE_NAME="Example Web Site"
ENV BANNER_COLOR=lightgray
ENV TIME_ZONE=UTC 
COPY website/html/* /var/www/example/
COPY website/conf/vhost-example.conf /etc/apache2/sites-available/
RUN a2ensite vhost-example
