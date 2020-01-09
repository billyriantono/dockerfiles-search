FROM richarvey/nginx-php-fpm:1.6.5

MAINTAINER AthrunJin <jinjiajun0910@gmail.com>

ENV SWOOLE_VERSION 4.3.0

RUN apk add --no-cache \
    gcc \
    g++ \
    make \
    autoconf \
    libc-dev \
    pcre

RUN docker-php-ext-install sockets

RUN CONFIG="\
  --enable-openssl \
  --enable-sockets \
  --enable-http2 --with-nghttp2-dir=/path/to \
  --enable-mysqlnd \
  --enable-async-redis --with-hiredis-dir=/path/to \
  " \
    && cd /home \
	&& curl -fSL https://github.com/swoole/swoole-src/archive/v$SWOOLE_VERSION.tar.gz -o swoole.tar.gz \
	&& tar -xzf swoole.tar.gz \
	&& rm -f swoole.tar.gz \
	&& cd swoole-src-$SWOOLE_VERSION \
	&& phpize \
	&& ./configure $CONFIG \
	&& make && make install


ADD php/docker-php-ext-swoole.ini /usr/local/etc/php/conf.d
ADD app/http-server.php /home/swoole/http-server.php



