ARG FLEXIFY_VERSION=latest
FROM flexifyio/management:$FLEXIFY_VERSION  AS management
FROM flexifyio/engine:$FLEXIFY_VERSION      AS engine
FROM flexifyio/web:$FLEXIFY_VERSION         AS web

FROM ubuntu:18.04

ENV FLEXIFY_DATA=/etc/flexify/data \
    FLEXIFY_DATA_SQL=/etc/flexify/data/sql \
    DB_PASSWORD='flexify' \
    LOGGING_LEVEL_IO_FLEXIFY=INFO \
    FLEXIFY_ENGINE_LOG_LEVEL=INFO

RUN set -ex; \
    # SSL certificates are stored in $FLEXIFY_DATA/ssl/, but are available from /etc/flexify/ssl/
    mkdir -p $FLEXIFY_DATA/ssl/; \
    ln -s $FLEXIFY_DATA/ssl/ /etc/flexify/; \
    # Engine logs are stored in /var/log/flexify/engine/, but are available from $FLEXIFY_DATA/engine/logs/
    mkdir -p $FLEXIFY_DATA/engine/; \
    mkdir -p /var/log/flexify/engine/; \
    ln -s -T /var/log/flexify/engine/ $FLEXIFY_DATA/engine/logs;  \
    groupadd -r mysql && useradd -r -g mysql mysql

WORKDIR /etc/flexify/

# All deps
RUN set -ex; \
    apt-get update; \
    apt-get install -y curl openssl; \
    curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | bash; \
    apt-get update; \
    apt-get install -y mariadb-server mariadb-backup; \
    apt-get install -y openjdk-11-jre; \
    apt-get install -y nginx; \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# MariaDB (copy-paste from https://github.com/docker-library/mariadb/blob/master/10.4/Dockerfile)
RUN set -ex; \
# purge and re-create /var/lib/mysql with appropriate ownership
	rm -rf /var/lib/mysql; \
	mkdir -p $FLEXIFY_DATA_SQL /var/run/mysqld; \
	chown -R mysql:mysql $FLEXIFY_DATA_SQL /var/run/mysqld; \
# ensure that /var/run/mysqld (used for socket and lock files) is writable regardless of the UID our mysqld instance ends up having at runtime
	chmod 777 /var/run/mysqld; \
# comment out a few problematic configuration values
	find /etc/mysql/ -name '*.cnf' -print0 \
        | xargs -0 grep -lZE '^(log)' \
        | xargs -rt -0 sed -Ei 's/^(log)/#&/'; \
# change datadir
    sed -ri 's/^datadir\s/#&/' /etc/mysql/my.cnf; \
    printf "[mysqld]\ndatadir = $FLEXIFY_DATA_SQL\n" >> /etc/mysql/conf.d/docker.cnf;

# Management server
COPY --from=management /management.jar                  /etc/flexify/management.jar

# Engine
COPY --from=engine \
    /etc/flexify/engine/flexify-engine \
    /etc/flexify/engine/cleanup-logs.sh                 /etc/flexify/engine/

# Nginx
RUN rm -rf /var/www/*; \
    rm -rf /usr/share/nginx/html/*; \
    rm -rf /etc/nginx/sites-enabled/*;

COPY --from=web /etc/nginx/conf.d/default.conf          /etc/nginx/conf.d/
COPY ./nginx/conf.d/                                    /etc/nginx/conf.d/

# web console config
COPY --from=web /etc/flexify/web/flexify-io/manage/     /etc/flexify/web/flexify-io/manage/
COPY ./web/conf.json                                    /etc/flexify/web/flexify-io/manage/conf/conf.json

# Our start and init scripts
COPY ./scripts/                                         /etc/flexify/
RUN chmod +x /etc/flexify/*.sh; \
    /etc/flexify/init-db.sh;

# General
VOLUME $FLEXIFY_DATA
EXPOSE 80 443
CMD ["/bin/bash", "-c", "/etc/flexify/start.sh"]

# Label at the end to make it the last year for eaiser updates
LABEL   vendor="Flexfiy.IO" \
        name="Flexify.IO Community Edition" \
        maintainer="support@flexify.io"
