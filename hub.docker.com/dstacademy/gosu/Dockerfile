FROM debian:9-slim as GOSU
MAINTAINER DST Academy <support@dst.academy>

# Set build arguments.
ARG GOSU_VERSION
ENV GOSU_VERSION ${GOSU_VERSION:-1.10}

# Install everything.
RUN set -ex \
	# Install dependencies.
	&& apt-get update \
	&& apt-get install -y --no-install-recommends wget ca-certificates gnupg2 dirmngr \
	# Install gosu.
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true

FROM debian:9-slim
MAINTAINER DST Academy <support@dst.academy>

# Install gosu.
COPY --from=GOSU /usr/local/bin/gosu /usr/local/bin/gosu

# Set default command.
CMD ["gosu"]
