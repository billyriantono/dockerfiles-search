FROM php:7.3.1-apache as frontend
EXPOSE 80
WORKDIR /var/www/html/
COPY . /var/www/html
CMD ["/usr/local/bin/apache2-foreground"]
