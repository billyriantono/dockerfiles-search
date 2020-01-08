FROM debian:jessie

MAINTAINER im@e11it.ru

ENV PGBADGER_VERSION=9.2
ENV PGBADGER_DATA=/data

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    wget \
    autoconf \
    automake \
    make \
    bzip2 \
    xz-utils \
    libtext-csv-xs-perl \
    libjson-xs-perl

RUN wget -O - https://github.com/dalibo/pgbadger/archive/v${PGBADGER_VERSION}.tar.gz | tar -zxvf - -C /tmp \
    && cd /tmp/pgbadger-${PGBADGER_VERSION} \
    && perl Makefile.PL INSTALLDIRS=vendor \
    && make \
    && make install \
    && rm -rf /tmp/pgbadger-${PGBADGER_VERSION}

COPY docker-entrypoint.sh /entrypoint.sh

VOLUME $PGBADGER_DATA

ENTRYPOINT ["/entrypoint.sh"]

CMD ["pgbadger"]
