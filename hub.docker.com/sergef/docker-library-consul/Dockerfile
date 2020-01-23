FROM sergef/docker-library-alpine:edge

EXPOSE 8300 8301 8302 8400 8500 8600
EXPOSE 8301/udp 8302/udp 8600/udp

ENV DOMAIN localhost.localdomain
ENV DATACENTER local

COPY entrypoint.sh /entrypoint.sh
COPY config /config

RUN apk add \
    --no-cache \
    consul@testing \
  && chmod +x /entrypoint.sh

ENTRYPOINT ["/sbin/tini", "--", "/entrypoint.sh"]
