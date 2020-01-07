FROM debian:stable-slim

ENV GOSU_VERSION 1.10
COPY entrypoint.sh /usr/local/bin/entrypoint.sh

RUN set -ex; \
	\
	fetchDeps=' \
		ca-certificates \
		wget \
		dirmngr gnupg \
	'; \
	apt-get update; \
	apt-get install -y --no-install-recommends $fetchDeps; \
	rm -rf /var/lib/apt/lists/*; \
	\
	dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"; \
	wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch"; \
	wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc"; \
	\
# verify the signature
	export GNUPGHOME="$(mktemp -d)"; \
	gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4; \
	gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu; \
	rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc; \
	\
	chmod +x /usr/local/bin/gosu; \
# verify that the binary works
	gosu nobody true; \
    chmod +x /usr/local/bin/entrypoint.sh; \
	\
	apt-get purge -y --auto-remove $fetchDeps

#RUN apt-get update && apt-get -y --no-install-recommends install \
#    ca-certificates \
#    curl \
#    dirmngr \
#    gnupg \
#    && rm -rf /var/lib/apt/lists/* \
#    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
#    &&  curl -o /usr/local/bin/gosu -SL \
#	"https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture)" \
#    && curl -o /usr/local/bin/gosu.asc -SL \
#	"https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture).asc" \
#    && gpg --verify /usr/local/bin/gosu.asc \
#    && rm /usr/local/bin/gosu.asc \
#    && chmod +x /usr/local/bin/gosu \
#    && apt-get purge -y --auto-remove gnupg dirmngr curl ca-certificates


ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
