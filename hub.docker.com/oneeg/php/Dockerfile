FROM oneeg/php:7.2-alpine3.8

RUN apk --update add \
    apache2 \
    php7-apache2@php \
    && rm -f /var/cache/apk/*

RUN mkdir /run/apache2 \
    && ln -sfT /dev/stderr "/var/log/apache2/error.log" \
    && ln -sfT /dev/stdout "/var/log/apache2/access.log"

RUN mkdir /app \
    && chown -R apache:apache /app \
    && chmod -R 755 /app \
    && mkdir /app/public

ADD httpd.conf /etc/apache2/httpd.conf
ADD site.conf /etc/apache2/conf.d/site.conf
ADD mpm.conf /etc/apache2/conf.d/mpm.conf

WORKDIR /app

EXPOSE 80

CMD ["httpd", "-D", "FOREGROUND"]
