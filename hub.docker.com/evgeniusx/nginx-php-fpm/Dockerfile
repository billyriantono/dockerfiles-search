FROM ubuntu:bionic
ENV PHP_VERSION=7.3 \
    PHP_REPO_KEY=14AA40EC0831756756D7F66C4F4EA0AAE5267A6C \
    PHP_REPO=http://ppa.launchpad.net/ondrej/php/ubuntu
RUN apt-get update -y && apt-get install -y  gpg
RUN echo "deb ${PHP_REPO} bionic main" > /etc/apt/sources.list.d/ondrej-ubuntu-php-bionic.list && \
    apt-key  adv --keyserver keyserver.ubuntu.com --recv-keys ${PHP_REPO_KEY} && \
    apt-get update -y && \
    apt-get install -y \
        php${PHP_VERSION}-fpm   \
        php${PHP_VERSION}-pdo   \
        php${PHP_VERSION}-json  \
        php${PHP_VERSION}-yaml  \
        php${PHP_VERSION}-xml   \
        php${PHP_VERSION}-mysql && \
    apt-get install -y nginx
RUN mkdir -p /var/run/php
COPY files/run.sh /run.sh
RUN chmod +x /run.sh
RUN rm -rf /var/lib/apt/lists/*
EXPOSE 80 443
CMD ["/run.sh"]