FROM alpine:latest
MAINTAINER "keoni84 - https://bitbucket.org/keoni84"
RUN addgroup -g 1025 nginx && addgroup -g 1026 www-data && addgroup -g 1020 mysql && \
adduser -u 1025 -G nginx -s /sbin/nologin -h /var/lib/nginx -D nginx && \
adduser -u 1026 -G www-data -s /sbin/nologin -h /var/lib/nginx -D webhost && \
adduser -u 1020 -G mysql -s /sbin/nologin -h /var/lib/mysql -D mysql && \
addgroup nginx www-data && addgroup webhost nginx && \
apk --no-cache add php7 php7-fpm php7-mysqli php7-json php7-openssl php7-curl \
php7-zlib php7-xml php7-phar php7-intl php7-dom php7-xmlreader php7-ctype \
php7-mbstring php7-gd supervisor tzdata mariadb mariadb-client nginx && \
cp /usr/share/zoneinfo/UTC /etc/localtime && echo UTC > /etc/timezone && \
mkdir /run/mysqld && chown mysql:mysql /run/mysqld && \
mysql_install_db --user=mysql --datadir=/var/lib/mysql && \
rm -f /var/lib/nginx/run && cd /var/lib/nginx && ln -s /var/run run
COPY supervisord.conf /etc/supervisord.conf
COPY nginx.conf /etc/nginx/nginx.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY php-www.conf /etc/php7/php-fpm.d/php-www.conf
COPY php.ini /etc/php7/php.ini
COPY index.html /var/lib/nginx/html/index.html
COPY phpinfo.php /var/lib/nginx/html/phpinfo.php
COPY 40x.html /var/lib/nginx/html/40x.html
COPY 50x.html /var/lib/nginx/html/50x.html
EXPOSE 80
VOLUME /var/log/nginx
VOLUME /var/lib/mysql
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]