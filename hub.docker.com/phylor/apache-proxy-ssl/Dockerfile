FROM debian

RUN apt-get update && apt-get install -y \
  apache2

RUN a2enmod ssl proxy proxy_http

CMD ["apachectl", "-DFOREGROUND"]

