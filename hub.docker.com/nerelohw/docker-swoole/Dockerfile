FROM nerelohw/docker-php7

ENV YAF_VERSION 3.0.7
ENV YAF_DOWNLOAD_URL https://github.com/laruence/yaf/archive/yaf-$YAF_VERSION.tar.gz

ENV SWOOLE_VERSION 4.1.2
ENV SWOOLE_DOWNLOAD_URL https://github.com/swoole/swoole-src/archive/v$SWOOLE_VERSION.tar.gz

RUN apk add -U libressl hiredis nghttp2 libpq \ 
&& apk add -U --virtual build-deps nghttp2-dev libaio-dev autoconf build-base linux-headers git libressl-dev hiredis-dev postgresql-dev \ 
&& cd /tmp/ \
&& wget -qO- $YAF_DOWNLOAD_URL | tar xvz \
&& cd yaf-yaf-$YAF_VERSION \
&& phpize \
&& ./configure --prefix=/usr  \
&& make && make install \
&& wget -qO- $SWOOLE_DOWNLOAD_URL | tar xvz \
&& cd swoole-src-$SWOOLE_VERSION \
&& phpize \
&& ./configure --prefix=/usr --enable-http2 --enable-sockets --enable-async-redis --enable-mysqlnd --enable-coroutine-postgresql --enable-openssl \
&& make && make install \
&& cd ~ \
&& rm -rf /tmp/* \
&& pecl install inotify msgpack \
&& apk del -U build-deps \
&& rm -rf /var/cache/apk/* 


RUN echo "extension=yaf.so" > /etc/php7/conf.d/yaf.ini \
&& echo "yaf.use_namespace=1" >> /etc/php7/conf.d/yaf.ini \
&& echo "extension=swoole.so" > /etc/php7/conf.d/swoole.ini \
&& echo "extension=inotify.so" > /etc/php7/conf.d/inotify.ini \
&& echo "extension=msgpack.so" > /etc/php7/conf.d/msgpack.ini


