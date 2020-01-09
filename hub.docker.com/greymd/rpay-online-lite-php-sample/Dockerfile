# This file is for production deployment.
FROM php:7.0-apache

COPY init.sh /

RUN apt-get update \
    && apt-get install -y git

EXPOSE 80
CMD ["bash","/init.sh","apache2-foreground"]
