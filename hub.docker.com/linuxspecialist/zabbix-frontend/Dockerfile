FROM alpine:3.4

MAINTAINER dennis@linux-specialist.nl

# Install packages
RUN apk update && \
    apk add php5-apache2 \
            apache2 \
            gettext \
            bash \
            curl \
            php5-cli \
            php5-curl \
            php5-dom \
            php5-gd \
            php5-fpm \
            php5-json \
            php5-mcrypt \
            php5-mysqli \
            php5-phar \
            php5-openssl \
            zabbix-webif && \
    rm -f /var/cache/apk/* && \
    mkdir -p /run/apache2 && \
    chmod -R 777 /run/apache2 && \
    ln -sf /dev/stdout /var/log/apache2/access.log && \
    ln -sf /dev/stderr /var/log/apache2/error.log


EXPOSE 80

COPY docker-entrypoint.sh /
COPY zabbix.conf.php.env /zabbix.conf.php.env
COPY zabbix-php.ini /etc/php5/conf.d/zabbix.ini
COPY apache-zabbix.conf /etc/apache2/conf.d/zabbix.conf

ENTRYPOINT ["/docker-entrypoint.sh"]
