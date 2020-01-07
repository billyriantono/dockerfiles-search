FROM jaredreisinger/postgres-12beta3-alpine-dev:latest as builder

#ENV HASHIDS_FORK iCyberon
ENV HASHIDS_FORK JaredReisinger
ENV HASHIDS_VERSION 1.2.1-fix

RUN set -ex \
	\
	&& wget -O pg_hashids.tar.gz https://github.com/$HASHIDS_FORK/pg_hashids/archive/v$HASHIDS_VERSION.tar.gz \
	&& mkdir -p /usr/src/postgresql/contrib/pg_hashids \
	&& tar \
		--extract \
		--file pg_hashids.tar.gz \
		--directory /usr/src/postgresql/contrib/pg_hashids \
		--strip-components 1 \
	&& rm pg_hashids.tar.gz \
	&& cd /usr/src/postgresql/contrib/pg_hashids \
	&& make install

# copy the built output into a clean postgres image
FROM postgres:12-beta3-alpine

COPY --from=builder /usr/local/lib/postgresql/pg_hashids* /usr/local/lib/postgresql/
COPY --from=builder /usr/local/share/postgresql/extension/pg_hashids* /usr/local/share/postgresql/extension/
