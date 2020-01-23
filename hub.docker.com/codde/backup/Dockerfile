FROM ruby:2.2-slim

ENV VERSION=0.1
ENV BACKUP_VERSION=4.1.12
ENV PG_MAJOR 9.5
ENV PG_VERSION 9.5.0-1.pgdg80+2

# Add pgSQL keys
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

# Add pgSQL repo
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' $PG_MAJOR > /etc/apt/sources.list.d/pgdg.list

RUN apt-get update \
  && apt-get -y install build-essential postgresql-common postgresql-client \
  && gem install backup -v "$BACKUP_VERSION" --no-ri --no-rdoc \
  && apt-get remove -y --purge build-essential && apt-get autoremove -y \
  && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY entrypoint.sh /entrypoint
COPY backup.sh /usr/local/bin/backup

ENTRYPOINT ["/entrypoint"]
