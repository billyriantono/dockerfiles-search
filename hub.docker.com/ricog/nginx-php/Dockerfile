FROM nginx:1.13
MAINTAINER Rick Guyer <ricoguyer@gmail.com>

COPY nginx.conf /etc/nginx/nginx.conf
ADD entrypoint.sh /usr/sbin/

ENV PHP_ADDR php:9000
ENV APP_ENV docker
ENV APP_ROOT /var/www/site/webroot
ENV APP_INDEX index.php

ENTRYPOINT ["entrypoint.sh"]
CMD ["nginx"]
