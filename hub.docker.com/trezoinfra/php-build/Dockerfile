FROM trezoinfra/php-fpm:7.2

RUN apt-get update \
    && apt-get install --no-install-recommends -y  awscli pbzip2 redis-server \
    && rm -Rf /var/lib/apt/lists/* \
    && groupadd -g 116 jenkins \
    && useradd -u 111 jenkins -g jenkins \
    && find /etc/php/ -iname "*xdebug*" | xargs rm -f {}
RUN mkdir -p /var/lib/redis && rm -Rf /var/cache/* \
    && touch /var/log/redis/redis-server.log \
    && chown redis:redis /var/log/redis/redis-server.log
COPY redis.conf /

RUN chown jenkins:jenkins redis.conf && service redis-server start
RUN chmod 775 -R /var/log/redis/
