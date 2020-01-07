FROM debian:stretch
RUN set -x \
	&& echo 'deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main' >> /etc/apt/sources.list.d/pgdg.list \
	&& apt-get update \
	&& apt-get upgrade -y \
	&& apt-get install -y gnupg gnupg2 wget \
	&& wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | apt-key add - \
	&& apt-get update \
	&& apt-get install -y gosu postgresql-10 \
	&& apt-get clean -y
ENV PG_MAJOR 10
ENV PGDATA /var/lib/postgresql/data
ENV PATH $PATH:/usr/lib/postgresql/$PG_MAJOR/bin
RUN set -ex \
	&& mv -v "/usr/share/postgresql/$PG_MAJOR/postgresql.conf.sample" /usr/share/postgresql/ \
	&& ln -sv /usr/share/postgresql/postgresql.conf.sample "/usr/share/postgresql/$PG_MAJOR/" \
	&& sed -ri "s!^#?(listen_addresses)\s*=\s*\S+.*!\1 = '*'!" /usr/share/postgresql/postgresql.conf.sample \
	&& mkdir -p "$PGDATA" && chown -R postgres:postgres "$PGDATA" && chmod 777 "$PGDATA"

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
EXPOSE 5432
CMD ["postgres"]
