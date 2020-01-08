FROM php:7.0-fpm-alpine

ENV PHALCON_VERSION=3.1.2
ENV PHALCON_DEV_TOOLS_VERSION=3.2.0

# Compile Phalcon
RUN set -xe && \
        # Add virtual packages. It will remove when done.
        apk add --no-cache --virtual .build-deps autoconf g++ make pcre-dev && \
        curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz && \
        tar xzf v${PHALCON_VERSION}.tar.gz && cd cphalcon-${PHALCON_VERSION}/build && sh install && \
        docker-php-ext-enable phalcon && \
        cd ../.. && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION} && \
        #REDIS
        pecl install redis && \
        docker-php-ext-enable redis && \
        rm -rf /var/cache/apk/* && \

        apk del .build-deps

#AWS SDK requirements
RUN docker-php-ext-install opcache

#http://docs.aws.amazon.com/aws-sdk-php/v3/guide/getting-started/
#http://docs.aws.amazon.com/aws-sdk-php/v3/api/
#https://github.com/phpredis/phpredis