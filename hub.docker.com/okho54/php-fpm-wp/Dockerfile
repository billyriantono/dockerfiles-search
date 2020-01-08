FROM ubuntu:bionic

LABEL maintainer="Artem Bokhan <abokhan@setronica.net>"
LABEL description="Php-fpm container"

VOLUME /var/www

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && \
    apt-get install -y software-properties-common curl mariadb-client && \
    LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y php7.2-fpm php7.2-cli php7.2-xml php7.2-mysql php7.2-curl \
    php7.2-gd php7.2-opcache php7.2-json php7.2-mbstring && \
    apt-get clean

RUN mv /etc/php/7.2/fpm/pool.d/www.conf /etc/php/7.2/fpm/pool.d/www.conf.off && \
    mv /etc/php/7.2/fpm/php-fpm.conf /etc/php/7.2/fpm/php-fpm.conf.off && \
    mkdir -p /var/log/php

RUN cd /tmp && curl -sLO https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    cp wp-cli.phar /usr/bin/wp && chmod +x /usr/bin/wp

COPY files /

CMD ["php-fpm7.2"]
