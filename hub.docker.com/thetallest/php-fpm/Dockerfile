FROM php:7.0.33-fpm-alpine

RUN apk add autoconf make g++ curl-dev libxml2-dev && \
    pecl install solr && \
    apk del autoconf make g++ curl-dev libxml2-dev && \
    docker-php-ext-enable solr
