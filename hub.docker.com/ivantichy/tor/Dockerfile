FROM debian:stretch

RUN apt-get update -y -q && apt-get install tor -y -q && rm -rf /var/lib/apt/lists/*

COPY test.sh /test.sh

COPY docker-entrypoint.sh /entrypoint.sh

RUN /test.sh

EXPOSE 6000 6001

ENTRYPOINT ["/entrypoint.sh"]

