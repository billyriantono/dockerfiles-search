FROM hyperwenzel/quantavidirectus-base-layer:1.0
MAINTAINER Krzysztof Wincel "kw@quantavi.com"

RUN get-directus 1.0
RUN composer install -o -d /var/www/html/
RUN fix-directus-permissions
