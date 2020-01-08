FROM wordpress:latest

MAINTAINER Marco Egger <m.egger@coozzy.com>

# Enable some modules
RUN a2enmod headers ssl http2

CMD ["apache2-foreground"]
