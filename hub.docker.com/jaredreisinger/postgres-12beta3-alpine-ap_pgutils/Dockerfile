FROM jaredreisinger/postgres-12beta3-alpine-dev:latest as builder

# ap_pgutils's makefile clones the phc-winner-argon2 repo, but we don't have
# git available in this image... we can just 'wget' the current code, though!
#
# Also, ap_pgutils's makefile hard-codes PG_HOME to something different from
# this image's PG_HOME, so we fix that up just before doing the 'make install'.
RUN set -ex \
	\
	&& wget -O ap_pgutils.zip https://github.com/Apsalar/ap_pgutils/archive/master.zip \
	&& wget -O argon2.zip https://github.com/Apsalar/phc-winner-argon2/archive/master.zip \
	&& mkdir -p /usr/src/postgresql/contrib/ap_pgutils/argon2 \
	&& unzip -d /usr/src/postgresql/contrib/ap_pgutils ap_pgutils.zip \
	&& unzip -d /usr/src/postgresql/contrib/ap_pgutils/argon2 argon2.zip \
	&& rm ap_pgutils.zip argon2.zip \
	&& cd /usr/src/postgresql/contrib/ap_pgutils \
	&& mv ap_pgutils-master/* . \
	&& mv argon2/phc-winner-argon2-master/* argon2/. \
	&& rm -r ap_pgutils-master argon2/phc-winner-argon2-master \
	&& sed -i 's/^PG_HOME=.*$/PG_HOME=\/usr\/local/' GNUmakefile \
	&& make install

# copy the built output into a clean postgres image
FROM postgres:12-beta3-alpine

COPY --from=builder /usr/local/lib/postgresql/ap_pgutils* /usr/local/lib/postgresql/
COPY --from=builder /usr/local/share/postgresql/extension/ap_pgutils* /usr/local/share/postgresql/extension/
