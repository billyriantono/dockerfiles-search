FROM conchoid/docker-phpenv-builtins:v1-12-5x-stretch AS php5
FROM conchoid/docker-phpenv-builtins:v1-12-7x-stretch AS php7
FROM conchoid/docker-phpenv:v1-12-5.6-stretch

ENV PHP_CONFIGURE_OPTS "--disable-fpm --disable-cgi"
ENV PHP_AUTOCONF /usr/bin/autoconf2.59

COPY --from=php5 ${PHPENV_ROOT}/versions/ ${PHPENV_ROOT}/versions/
COPY --from=php7 ${PHPENV_ROOT}/versions/ ${PHPENV_ROOT}/versions/

RUN phpenv global system \
    && phpenv versions
