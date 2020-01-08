FROM php:5.6.6-apache

RUN apt-get update && \
apt-get install -y tzdata && \
ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
dpkg-reconfigure -f noninteractive tzdata

RUN a2enmod proxy_fcgi rewrite

COPY apache2.conf /etc/apache2/apache2.conf

EXPOSE 80
CMD ["apache2-foreground"]
