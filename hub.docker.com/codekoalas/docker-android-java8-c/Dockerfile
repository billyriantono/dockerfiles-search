FROM php:7.3-cli-alpine

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

RUN mkdir -p /usr/local/env && ln -s /usr/local/bin/php /usr/local/env/php7.3
RUN apk update \ 
    && apk add wget \
    && apk add --no-cache \
        $PHPIZE_DEPS 
RUN pecl install redis && docker-php-ext-enable redis
ENV PATH  /usr/local/env:$PATH

ENTRYPOINT ["/entrypoint.sh"]
CMD [ "polar" ]