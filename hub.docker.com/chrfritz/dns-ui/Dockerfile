FROM php:7.4-apache-buster

RUN apt-get update && \
    apt-get install -y --no-install-recommends git libpq-dev libldap2-dev libsasl2-dev libicu-dev && \
    docker-php-ext-install pdo_pgsql pgsql ldap intl &&\
    rm -rf /var/lib/apt/lists/*

ENV APACHE_DOCUMENT_ROOT /dns-ui/public_html/

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf && \
    sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

RUN git clone https://github.com/operasoftware/dns-ui.git /dns-ui && \
    chown -R www-data:www-data /dns-ui

WORKDIR /dns-ui/public_html/
VOLUME /dns-ui/config/
