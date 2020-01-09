FROM nerelohw/docker-python3 

ENV PGADMIN4_VERSION 2.1

RUN set -ex \
	&& apk add --no-cache --virtual .run-deps \
		postgresql \
		postgresql-libs \
	&& apk add --no-cache --virtual .build-deps \
		gcc \
		musl-dev \
		openssl \
        python3-dev \
		postgresql-dev \
	&& pip --no-cache-dir install --default-timeout=100 \
		https://ftp.postgresql.org/pub/pgadmin/pgadmin4/v${PGADMIN4_VERSION}/pip/pgadmin4-${PGADMIN4_VERSION}-py2.py3-none-any.whl \
	&& apk del .build-deps

VOLUME /var/lib/pgadmin4

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod a+x /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 5050
CMD ["pgadmin4"]
