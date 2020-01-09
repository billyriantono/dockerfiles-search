FROM debian:buster

RUN apt-get update \
 && apt-get dist-upgrade -y \
 && apt-get install -y --no-install-recommends quassel-core \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /var/lib/quassel/*  # cleanup cert

VOLUME /var/lib/quassel

COPY docker-entrypoint /
COPY quasselcore /usr/local/bin/quasselcore

ENTRYPOINT ["/docker-entrypoint"]
CMD ["quasselcore"]
