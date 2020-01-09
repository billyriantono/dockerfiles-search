FROM codete/php5

MAINTAINER Codete <ci@codete.com>

RUN (curl -sS https://getcomposer.org/installer | php) && \
    chmod +x composer.phar && \
    mv composer.phar /usr/local/bin/composer

WORKDIR /srv

ENTRYPOINT ["composer"]
