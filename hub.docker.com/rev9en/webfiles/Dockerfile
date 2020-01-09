FROM alpine:3.9

ENV WWW_ROOT=/var/www/html

COPY /root /

RUN apk add --no-cache apache2 apache2-utils \
        php7 php7-apache2 php7-fpm php7-common php7-session php7-json php7-exif php7-gd \
    && ln -sf /proc/self/fd/1 /var/log/apache2/access.log \
    && ln -sf /proc/self/fd/1 /var/log/apache2/error.log \
    && sed -i "s/AllowOverride None/AllowOverride All/g" /etc/apache2/httpd.conf \
    && sed -i "/mod_rewrite.so/s/#LoadModule/LoadModule/" /etc/apache2/httpd.conf \
    \
    && sed -i 's/\/var\/www\/localhost\/htdocs/\/var\/www\/html/g' /etc/apache2/httpd.conf \
    \
    && apk add --no-cache zip ffmpeg imagemagick

ENTRYPOINT ["/entrypoint.sh"]

