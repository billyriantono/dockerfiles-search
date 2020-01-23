FROM 1and1internet/debian-9
MAINTAINER brian.wilkinson@1and1.co.uk
COPY --from=configurability_mysql /go/src/github.com/1and1internet/configurability/bin/plugins/mysql.so /opt/configurability/goplugins
ARG PGVER=9.6

# Installation
RUN export DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
	&& apt-get update \
	&& apt-get install -y curl gnupg sudo \
	&& curl -s https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
	&& apt-get update \
	&& apt-get install -y postgresql-${PGVER} \
	&& apt-get remove curl gnupg \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /tmp/*

COPY files/ /

# Post installation configuration
RUN cp /opt/postgresql/bash_profile /var/lib/postgresql/.bash_profile \
	&& chown postgres:postgres /var/lib/postgresql/.bash_profile \
	&& mkdir /var/run/postgresql/${PGVER}-main.pg_stat_tmp \
	&& chown postgres:postgres /var/run/postgresql/${PGVER}-main.pg_stat_tmp \
	&& chmod +x /usr/local/bin/run_postgres \
	&& chmod -R 755 /init /hooks \
	&& chmod 440 /etc/sudoers.d/postgres \
	&& cd /etc/postgresql/${PGVER}/main

ENV PATH=$PATH:/usr/lib/postgresql/${PGVER}/bin \
	PGVER=${PGVER} \
	PG_BIN=/usr/lib/postgresql/${PGVER}/bin \
	PG_DBDIR=/var/lib/postgresql/${PGVER}/main \
	LOCAL_AUTH_METHOD=password \
    HOST_AUTH_METHOD=password

VOLUME /var/lib/postgresql/${PGVER}
#EXPOSE 5432
