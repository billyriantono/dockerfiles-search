FROM ubuntu:trusty

RUN apt-get update && \
    apt-get install software-properties-common -y && \ 
    apt-get install -y language-pack-en-base && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install --yes --force-yes \
    nginx \
    php7.0 \
    php7.0-fpm \
    php7.0-ldap \
    php7.0-xml \
    phpldapadmin \
    slapd \
    ldap-utils

COPY entrypoint.sh /entrypoint.sh
COPY phpldapadmin-nginx /etc/nginx/sites-enabled/default
COPY config.php /usr/share/phpldapadmin/config/config.php
COPY phpldapadmin/TemplateRender.php /usr/share/phpldapadmin/lib/TemplateRender.php

VOLUME [ "/var/lib/ldap" ]

RUN ["chmod", "+x", "/entrypoint.sh"]

EXPOSE 80 389

ENTRYPOINT ["/entrypoint.sh"]
