FROM a3technology/php-fpm
RUN apk --update add tar autoconf make gcc musl-dev \
 && rm -rf /var/cache/apk/*
RUN  mkdir -p xdebug \
	&& wget -O - https://xdebug.org/files/xdebug-2.6.0beta1.tgz | tar -zxf - -C xdebug  --strip-components=1
RUN cd xdebug \ 
    && phpize \ 	
	&& ./configure --enable-xdebug \
	&& make -j$(nproc) \
	&& make install
RUN rm -r xdebug \
    && docker-php-ext-enable xdebug
RUN apk del tar autoconf make gcc musl-dev
COPY xdebug.ini /usr/local/etc/php/conf.d/
RUN chmod 777 /usr/local/etc/php/conf.d/xdebug.ini