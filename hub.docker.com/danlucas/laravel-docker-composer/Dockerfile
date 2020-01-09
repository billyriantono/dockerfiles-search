FROM danlucas/laravel-docker-base:0.1.0

MAINTAINER "Daniel Lucas" <daniel.chris.lucas@gmail.com>

USER root

WORKDIR /tmp

RUN apt-get update -y && \
    apt-get install -y curl \
    ca-certificates \
    git \
    php5-cli \
    php5-curl \
    php5-mcrypt \
    php5-gd && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    composer self-update && \
    apt-get remove --purge curl -y && \
    apt-get clean

RUN mkdir -p /data/www && \
    chown -R developer:staff /data/www

VOLUME ["/data"]
WORKDIR /data/www

USER developer

ENTRYPOINT ["composer"]
CMD ["--help"]
