FROM alpine:edge

LABEL maintainer="jason@ciandt.com"

ENV COMPOSER_VERION 1.7.2

RUN apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community  add \
    bash \
    curl \
    git \
    unzip \
    php7 \
    php7-xml \
    php7-simplexml \
    php7-zip \
    php7-xmlreader \
    php7-zlib \
    php7-opcache \
    php7-mcrypt \
    php7-openssl \
    php7-curl \
    php7-json \
    php7-dom \
    php7-phar \
    php7-mbstring \
    php7-ctype \
    && rm -rf /var/cache/apk/* \
    # Install Composer
	&& curl -sSL https://github.com/composer/composer/releases/download/$COMPOSER_VERION/composer.phar -o /usr/local/bin/composer && chmod +x /usr/local/bin/composer

COPY composer.json /opt/behat/composer.json

RUN \
	# Install Behat
	cd /opt/behat && \
	composer install 2>&1

ENV PATH $PATH:/opt/behat/bin

WORKDIR /src

ENTRYPOINT ["behat"]
