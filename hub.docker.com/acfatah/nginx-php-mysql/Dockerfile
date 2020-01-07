FROM alpine:3.5

ENV DEVELOPMENT="false"

ENV MYSQL_ROOT_PASSWORD="mysql"
ENV MYSQL_DATABASE_PRODUCTION="production"
ENV MYSQL_DATABASE_DEVELOPMENT="development"
ENV MYSQL_USER="mysql"
ENV MYSQL_PASSWORD="mysql"

ENV NGINX_SERVER_NAME="localhost"

ENV COMPOSER_ALLOW_SUPERUSER=1

RUN \
  apk update && \
  apk upgrade && \
  \
  apk add --no-cache \
    \
    curl \
    mysql \
    mysql-client \
    nginx \
    \
    php7-bcmath \
    php7-bz2 \
    php7-calendar \
    php7-ctype \
    php7-curl \
    php7-dom \
    php7-fpm \
    php7-gd \
    php7-gmp \
    php7-iconv \
    php7-intl \
    php7-json \
    php7-mbstring \
    php7-mcrypt \
    php7-openssl \
    php7-pdo_mysql \
    php7-pdo_sqlite \
    php7-phar \
    php7-posix \
    php7-session \
    php7-soap \
    php7-sqlite3 \
    php7-xdebug \
    php7-xml \
    php7-xmlreader \
    php7-xmlrpc \
    php7-zip \
    php7-zlib \
  && \
  rm -fr /var/cache/apk/* && \
  ln -s /usr/bin/php7 /usr/bin/php && \
  ln -s /usr/sbin/php-fpm7 /usr/sbin/php-fpm && \
  \
  mkdir /tmp/composer && \
  curl -o /tmp/composer/composer-setup.php https://getcomposer.org/installer && \
  curl -o /tmp/composer/composer-setup.sig https://composer.github.io/installer.sig && \
  php -r \
"if (\
    hash(\
        'SHA384',\
        file_get_contents('/tmp/composer/composer-setup.php')\
    ) !== trim(\
        file_get_contents('/tmp/composer/composer-setup.sig')\
    )\
) {\
    unlink('/tmp/composer/composer-setup.php');\
    echo 'Invalid installer' . PHP_EOL; exit(1);\
}" && \
  php /tmp/composer/composer-setup.php \
    --install-dir=/usr/local/bin \
    --filename=composer && \
  composer selfupdate && \
  rm -fr /tmp/composer && \
  mv /etc/mysql/my.cnf /etc/mysql/my.cnf.bak && \
  mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak

COPY composer-setup.sh /tmp/setup/composer-setup.sh
COPY entrypoint.sh /entrypoint.sh
COPY mysql-setup.sh /tmp/setup/mysql-setup.sh
COPY nginx-setup.sh /tmp/setup/nginx-setup.sh
COPY php-fpm-setup.sh /tmp/setup/php-fpm-setup.sh

VOLUME /app
WORKDIR /app
EXPOSE 80 3306
CMD ["/entrypoint.sh"]