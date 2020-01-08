FROM composer/composer:php7
MAINTAINER Alex Davidovich <alxsad@gmail.com>

WORKDIR /tmp

RUN composer selfupdate && \
    composer require "phpspec/phpspec" --prefer-source --no-interaction && \
    ln -s /tmp/vendor/bin/phpspec /usr/local/bin/phpspec

VOLUME ["/app"]
WORKDIR /app

ENTRYPOINT ["/usr/local/bin/phpspec"]
CMD ["--help"]
