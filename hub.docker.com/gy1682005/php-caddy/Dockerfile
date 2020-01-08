FROM gy1682005/php-fpm:5.6
MAINTAINER tanghao <gy1682005@qq.com>

RUN yum install -y caddy && yum clean all

RUN mkdir -p /var/www/html &&\
    echo "<?php phpinfo();?>" > /var/www/html/index.php &&\
    chown -R apache:apache /var/www/html

COPY config/caddy.conf /etc/caddy/
COPY config/caddy.ini /etc/supervisord.d/

WORKDIR /var/www/html
EXPOSE 80 8080