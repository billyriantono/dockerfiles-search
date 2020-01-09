FROM alpine:3.8

LABEL maintainer="Cristian Mello <cristianc.mello@gmail.com>"

ARG BUILD_DATE
ARG VCS_REF
ARG RETHINKDB_VERSION=2.3.6

LABEL org.label-schema.build-date=$BUILD_DATE \
	org.label-schema.vcs-url="https://github.com/mterron/rethinkdb.git" \
	org.label-schema.vcs-ref=$VCS_REF \
	org.label-schema.schema-version="1.0.0-rc.1" \
	org.label-schema.version=$RETHINKDB_VERSION \
	org.label-schema.description="Alpine based RethinkDB image"

RUN echo "Rethinkdb for Alpine Linux" && \
	apk --no-cache upgrade && \
	apk --no-cache add \
        rethinkdb \
        su-exec \
        supervisor \
		'nodejs-npm<8.11.4' \
    && mkdir /data && \
	apk --no-cache info -v | sed "s/-r\d*$//g"|sed 's/\(.*\)-/\1 /' > /etc/manifest.txt && \
    mkdir -p /var/log/supervisor

ADD conf/supervisord.conf /etc/supervisord.conf

VOLUME ["/data"]

WORKDIR /data

COPY entrypoint.sh /
COPY start-rethinkdb.sh /

COPY ./scripts/rethinkdb-entrypoint-db.init.sh /rethinkdb-entrypoint-db.init.sh

ENTRYPOINT /entrypoint.sh

# Ports:	process cluster webui
EXPOSE	    28015 	29015 	8080