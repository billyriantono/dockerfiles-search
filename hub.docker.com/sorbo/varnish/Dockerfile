#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "update.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
FROM debian:stretch-slim

ENV VARNISH_VERSION 4.1.11-1~stretch

RUN set -eux; \
    fetchDeps=" \
        curl \
        gnupg \
    "; \
    apt-get update; \
    apt-get install -y --no-install-recommends --no-install-suggests debian-archive-keyring apt-transport-https ca-certificates $fetchDeps; \
    curl -L https://packagecloud.io/varnishcache/varnish41/gpgkey | apt-key add -; \
    echo deb https://packagecloud.io/varnishcache/varnish41/debian stretch main > /etc/apt/sources.list.d/varnish.list; \
    apt-get update; \
    apt-get install -y --no-install-recommends --no-install-suggests varnish=$VARNISH_VERSION; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $fetchDeps; \
    rm -rf /var/lib/apt/lists/*; \
    rm -rf /tmp/*

WORKDIR /etc/varnish

COPY docker-varnish-entrypoint /usr/local/bin/
ENTRYPOINT ["docker-varnish-entrypoint"]

EXPOSE 80
CMD ["varnishd", "-F", "-f", "/etc/varnish/default.vcl"]
