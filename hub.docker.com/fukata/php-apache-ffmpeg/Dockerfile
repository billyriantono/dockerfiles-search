FROM webdevops/php-apache:alpine-php7
MAINTAINER Tatsuya Fukata <tatsuya.fukata@gmail.com>

RUN set -x \
    # Install apache
    && apk-install \
        ffmpeg \
    && docker-run-bootstrap \
    && docker-image-cleanup
