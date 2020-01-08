FROM m0elnx/alpine-x86:edge
MAINTAINER M0E-lnx@gmail.com

ENV PG_APP_HOME="/etc/docker-postgresql"\
    PG_VERSION=9.5 \
    PG_USER=postgres \
    PG_HOME=/var/lib/postgresql \
    PG_RUNDIR=/run/postgresql \
    PG_LOGDIR=/var/log/postgresql \
    PG_CERTDIR=/etc/postgresql/certs

ENV PG_BINDIR=/usr/bin/ \
    PG_DATADIR=${PG_HOME}/${PG_VERSION}/main

RUN apk add --no-cache acl postgresql bash sudo \
	&& cp /usr/share/postgresql/postgresql.conf.sample /usr/share/postgresql/postgresql.conf \
	&& cp /usr/share/postgresql/pg_hba.conf.sample /usr/share/postgresql/pg_hba.conf \
	&& cp /usr/share/postgresql/pg_ident.conf.sample /usr/share/postgresql/pg_ident.conf \
	&& ln -sf ${PG_DATADIR}/postgresql.conf /usr/share/postgresql/postgresql.conf \
	&& ln -sf ${PG_DATADIR}/pg_hba.conf /usr/share/postgresql/pg_hba.conf \
	&& ln -sf ${PG_DATADIR}/pg_ident.conf /usr/share/postgresql/pg_ident.conf \
	&& rm -rf ${PG_HOME}

COPY runtime/ ${PG_APP_HOME}/
COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh

EXPOSE 5432/tcp
VOLUME ["${PG_HOME}", "${PG_RUNDIR}"]
WORKDIR ${PG_HOME}
ENTRYPOINT ["/sbin/entrypoint.sh"]
