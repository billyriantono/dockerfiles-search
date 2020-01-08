FROM centos:centos7

RUN echo "Europe/Moscov" > /etc/timezone
RUN localedef -i ru_RU -f UTF-8 ru_RU.UTF-8

RUN groupadd -r postgres --gid=1000; \
	useradd -r -g postgres --uid=1000 --home-dir=/usr/local/pgsql --shell=/bin/bash postgres; \
	mkdir -p /usr/local/pgsql; \
	chown -R postgres:postgres /usr/local/pgsql

ENV GOSU_VERSION 1.10
RUN set -x && \
    curl -Lo /usr/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64" && \
    curl -Lo /tmp/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-amd64.asc" && \
    export GNUPGHOME="$(mktemp -d)" && \
    for server in $(shuf -e ha.pool.sks-keyservers.net \
                            hkp://p80.pool.sks-keyservers.net:80 \
                            keyserver.ubuntu.com \
                            hkp://keyserver.ubuntu.com:80 \
                            pgp.mit.edu) ; do \
        gpg --keyserver "$server" --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 && break || : ; \
    done && \
    gpg --batch --verify /tmp/gosu.asc /usr/bin/gosu && \
    rm -r "$GNUPGHOME" /tmp/gosu.asc && \
    chmod +x /usr/bin/gosu && \
    # Allow user to become root
    #chmod u+s /usr/bin/gosu && \
    gosu nobody true

RUN yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm 

RUN yum install -y postgresql11 postgresql11-server

RUN mkdir -p /var/run/postgresql \
	&& chown -R postgres:postgres /var/run/postgresql \
	&& chmod 2777 /var/run/postgresql

RUN mkdir -p /usr/local/pgsql/data \
	&& chown postgres:postgres /usr/local/pgsql/data \
	&& chmod 777 /usr/local/pgsql/data

RUN gosu postgres:postgres /usr/pgsql-11/bin/initdb --auth=trust --auth-host=trust --auth-local=trust -D /usr/local/pgsql/data -E UTF8

RUN echo "host all all 0.0.0.0/0 trust" >> /usr/local/pgsql/data/pg_hba.conf

RUN echo "listen_addresses = '*'" >> /usr/local/pgsql/data/postgresql.conf

VOLUME ["/usr/local/pgsql/data", "/var/run/postgresql"]

EXPOSE 5432

USER postgres

CMD ["/usr/pgsql-11/bin/postgres", "-D", "/usr/local/pgsql/data"]