FROM postgres:10

COPY ./sources.list /etc/apt/sources.list
ENV PG_CONFIG /usr/lib/postgresql/10/bin/pg_config
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        apt-utils curl make gcc build-essential \
        libicu-dev postgresql-server-dev-10 postgresql-10-jsquery \
        ca-certificates iputils-ping\
    && cd /tmp \
    && curl -L -O https://zh.osdn.net/dl/pgbigm/pg_bigm-1.2-20161011.tar.gz \
    && tar zxfv pg_bigm-1.2-20161011.tar.gz \
    && cd pg_bigm-1.2-20161011 \
    && make USE_PGXS=1 \
    && make USE_PGXS=1 install \
    && echo "shared_preload_libraries = 'pg_bigm'" >> /usr/share/postgresql/10/postgresql.conf.sample \
    && rm -rf /tmp/pg_bigm-1.2-20161011 \
    && apt-get purge -y curl make gcc apt-utils \
       build-essential libicu-dev postgresql-server-dev-10 \
    && apt-get clean

ENV PG_MAX_WAL_SENDERS 8
ENV PG_WAL_KEEP_SEGMENTS 8
COPY setup-replication.sh /docker-entrypoint-initdb.d/
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /docker-entrypoint-initdb.d/setup-replication.sh /docker-entrypoint.sh
