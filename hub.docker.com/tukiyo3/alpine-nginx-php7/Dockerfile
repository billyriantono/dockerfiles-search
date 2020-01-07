FROM alpine:3.5

RUN apk --update --no-cache add tzdata \
 && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
 && apk del tzdata

RUN apk --update --no-cache add nginx php7-fpm \
 && mkdir /run/nginx/

COPY ./conf/nginx.conf /etc/nginx/conf.d/default.conf
COPY ./conf/php-fpm7.conf /etc/php7/php-fpm.d/www.conf
COPY ./conf/php.ini /etc/php7/conf.d/php.ini
COPY ./www/index.php /var/www/localhost/htdocs/index.php

VOLUME /var/www/localhost/htdocs/
CMD sh -c "cd /usr/sbin; nginx; php-fpm7; crond -f -l 2"
