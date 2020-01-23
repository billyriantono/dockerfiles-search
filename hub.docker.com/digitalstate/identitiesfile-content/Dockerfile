FROM digitalcanvasdesign/php-fpm:latest

LABEL maintainer="Jason Raimondi <jason@raimondi.us>"

WORKDIR /usr/local/src

ENV PHPGEARMAN_NAME=gearman-2.0.3 \
    BUILD_DEPENDENCIES="\
        autoconf \
		dpkg-dev \
		file \
		g++ \
		gcc \
		libc-dev \
		libpcre3-dev \
		make \
		pkg-config \
		\
		ca-certificates \
        curl \
        libsqlite3-0 \
        xz-utils \
        wget \
        git" \
    RUN_DEPENDENCIES="\
		libboost-all-dev \
		libgearman-dev \
		gperf \
		libevent-dev \
		uuid-dev \
		libcloog-ppl-dev"

USER root

RUN apt-get update \
    && apt-get install -y --no-install-recommends $BUILD_DEPENDENCIES $RUN_DEPENDENCIES \
    && curl -fsSL "https://github.com/wcgallego/pecl-gearman/archive/$PHPGEARMAN_NAME.tar.gz" -o $PHPGEARMAN_NAME.tar.gz \
    && mkdir ./$PHPGEARMAN_NAME \
    && tar zxf $PHPGEARMAN_NAME.tar.gz  -C ./$PHPGEARMAN_NAME --strip-components=1 \
    && ( \
        cd $PHPGEARMAN_NAME \
        && phpize \
        && ./configure \
        && make \
        && make install \
    ) \
    && rm $PHPGEARMAN_NAME.tar.gz \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $BUILD_DEPENDENCIES \
    && apt-get clean

RUN apt-get install -y --no-install-recommends libgearman-dev

COPY ./gearman.ini /usr/local/etc/php/conf.d/gearman.ini

EXPOSE 9000

CMD ["php-fpm"]

USER www-data
