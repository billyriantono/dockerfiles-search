FROM php:7.3-apache

EXPOSE 80

RUN docker-php-ext-install mbstring pdo pdo_mysql  \
  && a2enmod rewrite expires headers

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

CMD ["apache2-foreground"]
