FROM drupalcomposer/drupal
MAINTAINER William Hearn <sylus1984@gmail.com>

ENV MONGO_PHP_DRIVER_VERSION 1.2.10
ENV TIDEWAYS_VERSION 4.1.2
ENV XHGUI_VERSION 0.8.1

RUN apk add --no-cache git

RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    openssl-dev \
    && git clone https://github.com/tideways/php-profiler-extension.git \
    && cd php-profiler-extension \
    && git checkout v${TIDEWAYS_VERSION} \
    && phpize \
    && ./configure \
    && make && make install && make clean \
    && git clone https://github.com/mongodb/mongo-php-driver.git $PHP_INI_DIR/mongo-php-driver \
    && cd $PHP_INI_DIR/mongo-php-driver \
    && git checkout ${MONGO_PHP_DRIVER_VERSION} \
    && git submodule sync \
    && git submodule update --init \
    && phpize \
    && ./configure \
    && make && make install && make clean \
    && apk del .build-deps

COPY conf/xhprof.ini $PHP_INI_DIR/conf.d/xhprof.ini

WORKDIR /var/www/xhgui

RUN curl -fSL "https://github.com/perftools/xhgui/archive/${XHGUI_VERSION}.tar.gz" -o xhgui.tar.gz \
	&& tar -xz --strip-components=1 -f xhgui.tar.gz \
	&& rm xhgui.tar.gz \
	&& chown -R www-data:www-data *

# Ports
EXPOSE 9000 27017

# Defaults
ENTRYPOINT ["php-fpm"]
