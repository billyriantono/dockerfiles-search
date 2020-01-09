FROM alpine:3.3
MAINTAINER Gabor Korodi (gkorodi@gmail.com)
WORKDIR /root

RUN apk update && apk add git
RUN apk add php \
  php-fpm \
  php-mcrypt \
  php-openssl \
  php-json \
  php-phar \
  php-zlib \
  php-dom \
  php-pdo \
  php-pdo_sqlite \
  php-mysql \
  php-mysqli \
  php-pdo_mysql \
  php-ctype

COPY install_composer.sh ./
RUN chmod 777 install_composer.sh
RUN git clone https://github.com/laravel/quickstart-basic.git
RUN ./install_composer.sh

# Build Laravel project
RUN cd /root/quickstart-basic; \
  php /root/composer.phar install; \
  awk '{ gsub("DB_HOST", "DB_CONNECTION=sqlite\nDB_HOST"); print}' .env.example > .env; \
  touch /root/quickstart-basic/database/database.sqlite; \
  php artisan migrate

RUN cd /root/quickstart-basic; \
  php artisan key:generate

EXPOSE 8000
WORKDIR /root/quickstart-basic
CMD ["php", "artisan", "serve", "--host", "0.0.0.0"]