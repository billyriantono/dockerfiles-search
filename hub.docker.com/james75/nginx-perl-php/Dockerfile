FROM ubuntu:16.04

## Install NGINX
RUN apt-get update && \
    apt-get install -y ca-certificates nginx-extras

RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

## Install Perl
RUN apt-get update && \
    apt-get install -y curl && \
    curl -L https://install.perlbrew.pl | bash

## Install PHP
RUN apt-get update && \
    apt-get install -y php-fpm php-mysql


VOLUME ["/var/cache/nginx"]

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]