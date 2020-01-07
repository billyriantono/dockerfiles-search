FROM postgres:9.6.9

ARG PATHMAN_VERSION=1.4.12
ARG PG_DEV_VERSION=9.6

# Add plugin

RUN set -x \
	&& apt-get update && apt-get install -y --no-install-recommends git gcc make ca-certificates wget unzip make libhiredis-dev libpq-dev postgresql-server-dev-$PG_DEV_VERSION gcc libc6-dev libssl-dev libkrb5-dev \
	&& mkdir -p /inst/ \
    && cd /inst \
    && git clone https://github.com/nahanni/rw_redis_fdw.git \
    && cd /inst/rw_redis_fdw \
    && PATH=/usr/local/postgresql/bin/:$PATH make USE_PGXS=1 \
    && PATH=/usr/local/postgresql/bin/:$PATH make USE_PGXS=1 install \
    && rm -Rf /inst \
    && wget -O /tmp/pg_pathman.zip https://github.com/postgrespro/pg_pathman/archive/$PATHMAN_VERSION.zip \
	&& unzip /tmp/pg_pathman.zip  -d /tmp \
    && cd /tmp/pg_pathman-$PATHMAN_VERSION \
    && make USE_PGXS=1 install \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get purge -y --auto-remove ca-certificates wget unzip make postgresql-server-dev-$PG_DEV_VERSION gcc libc6-dev libssl-dev libkrb5-dev \
    && rm -rf /tmp/pg_*

#Time
ENV TW=Asia/Taipei
RUN ln -snf /usr/share/zoneinfo/$TW /etc/localtime && echo $TW > /etc/timezone
