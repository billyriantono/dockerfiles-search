FROM alpine:3.5

RUN apk --no-cache add nginx supervisor curl zip unzip git \
        php7 php7-fpm php7-mcrypt php7-gd php7-pdo php7-pdo_mysql \
        php7-intl php7-phar php7-mbstring php7-xml php7-curl php7-exif php7-zlib \
        php7-json php7-zip php7-openssl php7-ctype php7-dom php7-pdo_sqlite php7-sqlite3 \
    && mkdir /run/php \
    && mkdir /run/nginx \
    && ln -sf /dev/null /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log \
    && sed -ie 's/;pid = run\/php-fpm7.pid/pid = \/run\/php-fpm7.pid/g' /etc/php7/php-fpm.conf \
    && sed -ie 's/;error_log = log\/php7\/error.log/error_log = \/proc\/self\/fd\/2/g' /etc/php7/php-fpm.conf \
    && sed -ie 's/;daemonize = yes/daemonize = no/g' /etc/php7/php-fpm.conf \
    && sed -ie 's/user = nobody/user = nginx/g' /etc/php7/php-fpm.d/www.conf \
    && sed -ie 's/group = nobody/group = nginx/g' /etc/php7/php-fpm.d/www.conf \
    && sed -ie 's/listen = 127\.0\.0\.1:9000/listen = \/run\/php\/php-fpm7.sock/g' /etc/php7/php-fpm.d/www.conf \
    && sed -ie 's/;listen.owner = nobody/listen.owner = nginx/g' /etc/php7/php-fpm.d/www.conf \
    && sed -ie 's/;listen.group = nobody/listen.group = nginx/g' /etc/php7/php-fpm.d/www.conf \
    && sed -ie 's/;catch_workers_output = yes/catch_workers_output = yes/g' /etc/php7/php-fpm.d/www.conf \
    && sed -ie 's/;clear_env = no/clear_env = no/g' /etc/php7/php-fpm.d/www.conf \
    && echo 'daemon off;' >> /etc/nginx/nginx.conf \
    && ln -s /usr/bin/php7 /usr/bin/php \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer --quiet

COPY supervisord.conf /etc/supervisord.conf

EXPOSE 80

CMD ["/usr/bin/supervisord"]
