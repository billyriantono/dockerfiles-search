FROM dylanlindgren/docker-phpcli:latest

WORKDIR /tmp

RUN apt-get update -y && \
    apt-get install -y curl git php5-mcrypt php5-gd php5-curl && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    apt-get remove --purge curl -y && \
    apt-get clean

VOLUME ["/app"]

WORKDIR /app

RUN sed -i 's/memory_limit = .*/memory_limit = '1024M'/' /etc/php5/cli/php.ini

ONBUILD RUN composer self-update

CMD ["-"]

ENTRYPOINT ["composer", "--ansi"]
