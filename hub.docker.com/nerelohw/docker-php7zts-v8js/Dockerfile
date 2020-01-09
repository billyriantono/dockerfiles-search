##6.8-edge
FROM nerelohw/docker-alpine-libv8:6.8-edge as libv8
##edge
FROM nerelohw/docker-php7zts 

COPY --from=libv8 /usr/local/v8 /usr/local/v8

RUN apk add -U --virtual .v8js-deps sudo tzdata git build-base \
&& cd /tmp \
&& git clone --branch=php7 https://github.com/phpv8/v8js.git \
&& cd v8js && phpize7 \
&& ./configure --with-v8js=/usr/local/v8 LDFLAGS="-lstdc++" \
&& make  && sudo make install \
&& echo "extension=v8js.so" > /etc/php7/conf.d/v8js.ini \
&& cp /usr/share/zoneinfo/UTC /etc/timezone \
&& sed -i "s/;date.timezone.*/date.timezone = 'UTC'/g" /etc/php7/php.ini \
&& apk del .v8js-deps \
&& rm -rf /var/cache/apk/* /tmp/*  
