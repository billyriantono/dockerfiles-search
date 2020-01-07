FROM alpine:3.8

LABEL maintainer="niuyuxian <ncc0706@gmail.com>"

ARG REDIS_VERSION=4.0.8

COPY rootfs /

RUN set -exo pipefail \
  && apk add --no-cache --virtual .build-deps \
    build-base \
    linux-headers \
    openssl \
  && wget -q -O /usr/local/bin/gosu https://github.com/tianon/gosu/releases/download/1.10/gosu-amd64 \
  && chmod +x /usr/local/bin/* \
  && cd /tmp \
  && wget -q -O - https://github.com/antirez/redis/archive/${REDIS_VERSION}.tar.gz  | tar -xzf - \
  && cd redis-${REDIS_VERSION} \
  && make && make install \
  && cp redis.conf /etc/redis.conf \
  && sed -i -e 's/bind 127.0.0.1/bind 0.0.0.0/' /etc/redis.conf \
  && adduser -D redis \
  && apk del .build-deps \
  && rm -rf /tmp/*


VOLUME ["/data"]

EXPOSE 6379

ENTRYPOINT ["entrypoint.sh"]
CMD ["redis-server", "/etc/redis.conf"]
