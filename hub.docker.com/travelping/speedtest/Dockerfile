FROM php:7.3.1-apache
EXPOSE 80
WORKDIR /var/www/html/
COPY *.php *.js *.png /var/www/html/
COPY telemetry/*.php /var/www/html/telemetry/
COPY index.html /var/www/html/index.html
COPY cennso-overlay/ /var/www/html/
RUN ln -s /var/www/html /var/www/html/speedtest
CMD ["/usr/local/bin/apache2-foreground"]
