FROM sbdev/laravel:laravel-1.7
RUN apt-get install -y wget
RUN wget -c "http://xdebug.org/files/xdebug-2.7.0.tgz" \
	&& tar -xf xdebug-2.7.0.tgz \
	&& rm xdebug-2.7.0.tgz \
	&& ( \
        cd xdebug-2.7.0 \
        && phpize \
        && ./configure --enable-xdebug \
        && make \
        && make install \
    ) \
  && rm -r xdebug-2.7.0 \
  && docker-php-ext-enable xdebug
#COPY config/docker-php-ext-xdebug.ini /usr/local/etc/php/conf.d/
#RUN useradd -ms /bin/bash ken
