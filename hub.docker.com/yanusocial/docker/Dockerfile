FROM ubuntu:14.04

MAINTAINER jose luis

LABEL version 1.0

RUN apt-get update && apt-get install -y \
apache2 \
php5 \
&& rm -rf /var/lib/apt/lists/* \
&& rm -f /var/www/html/*

COPY index.php /var/www/html

EXPOSE 80 443

ENTRYPOINT ["/usr/sbin/apache2ctl", "-DFOREGOUND"]
