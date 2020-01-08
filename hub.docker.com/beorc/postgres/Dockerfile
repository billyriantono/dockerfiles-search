FROM ubuntu:trusty

ENV PG_VERSION 9.4
ENV PG_HOME /var/lib/postgresql
ENV PG_RUNDIR /run/postgresql
ENV PG_LOGDIR /var/log/postgresql
ENV DB_LOCALE en_US.UTF-8

ENV PG_CONFDIR "/etc/postgresql/${PG_VERSION}/main"
ENV PG_BINDIR "/usr/lib/postgresql/${PG_VERSION}/bin"
ENV PG_DATADIR "${PG_HOME}/${PG_VERSION}/main"

RUN apt-get update -qq && apt-get install -y locales wget

RUN dpkg-reconfigure locales && \
    locale-gen $DB_LOCALE && \
    locale-gen en_US.UTF-8 && \
    /usr/sbin/update-locale LANG=en_US.UTF-8

RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
 && echo 'deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y postgresql-${PG_VERSION} postgresql-client-${PG_VERSION} postgresql-contrib-${PG_VERSION} \
 && rm -rf ${PG_HOME} \
 && rm -rf /var/lib/apt/lists/*

COPY docker-entrypoint.sh /sbin/docker-entrypoint.sh
RUN chmod 755 /sbin/docker-entrypoint.sh

EXPOSE 5432/tcp
VOLUME $PG_HOME $PG_LOGDIR
ENTRYPOINT ["/sbin/docker-entrypoint.sh"]
CMD ["postgres"]
