FROM apptechdev/php-fpm

WORKDIR /tmp

RUN apt-get update -qq && \
    apt-get install -yq \
        imagemagick \
        libicu-dev \
        libmagickcore-dev \
        libmagickwand-dev \
        libmcrypt-dev \
        libpng-dev

RUN curl -sL "https://github.com/mkoppanen/imagick/archive/3.3.0.tar.gz" -o "imagick.tar.gz" && \
    tar xfz ./imagick.tar.gz && \
    mv ./imagick-* /usr/src/php/ext/imagick

RUN curl -sL "https://github.com/phpredis/phpredis/archive/2.2.7.tar.gz" -o "redis.tar.gz" && \
    tar xfz ./redis.tar.gz && \
    mv ./phpredis-* /usr/src/php/ext/redis

RUN docker-php-ext-install \
        bcmath \
        gd \
        iconv \
        imagick \
        intl \
        mbstring \
        mcrypt \
        mysqli \
        opcache \
        pdo_mysql \
        redis

RUN touch $APP_LOGS/debug.log && \
    touch $APP_LOGS/error.log && \
    touch $APP_LOGS/queries.log && \
    touch $APP_LOGS/search.log && \
    touch $APP_LOGS/tracer.log && \
    touch $APP_LOGS/xdebug.log && \
    chown -R $APP_USER:$APP_USER $APP_LOGS

RUN apt-get autoremove -yq && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/www/*

COPY ./start.sh /var/www/start.sh

WORKDIR $APP_ROOT

CMD /var/www/start.sh
