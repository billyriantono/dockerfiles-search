FROM sumglobal/rpi-openjdk:8-azul

RUN [ "cross-build-start" ]

# explicitly set user/group IDs
RUN groupadd -r cassandra --gid=999 && useradd -r -g cassandra --uid=999 cassandra

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.7
RUN set -x \
	&& apt-get update && apt-get install -y --no-install-recommends \
           ca-certificates \
           wget \
           python \
           python-dev \
           python-pip \
           python-virtualenv \
        && rm -rf /var/lib/apt/lists/* \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
	&& export GNUPGHOME="$(mktemp -d)" \
	&& gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
	&& gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
	&& rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu \
	&& gosu nobody true \
	&& apt-get purge -y --auto-remove ca-certificates 

# solves warning: "jemalloc shared library could not be preloaded to speed up memory allocations"
RUN apt-get update && apt-get install -y --no-install-recommends libjemalloc1 && rm -rf /var/lib/apt/lists/*

ENV CASSANDRA_VERSION 3.11.0
ENV DISTRO_NAME "apache-cassandra-$CASSANDRA_VERSION"

RUN set -x \
    && wget "http://www.gtlib.gatech.edu/pub/apache/cassandra/$CASSANDRA_VERSION/$DISTRO_NAME-bin.tar.gz" \
    && tar -xzf "$DISTRO_NAME-bin.tar.gz" \
    && rm -r "$DISTRO_NAME-bin.tar.gz"

ENV CASSANDRA_CONFIG "/$DISTRO_NAME/conf"
ENV CASSANDRA_CONF "/$DISTRO_NAME/conf"
ENV MAX_HEAP_SIZE "256m"
ENV HEAP_NEWSIZE "128m"
ENV CASSANDRA_START_RPC "true"


COPY docker-entrypoint.sh /docker-entrypoint.sh
COPY cassandra.yaml /$CASSANDRA_CONFIG/
ENTRYPOINT ["/docker-entrypoint.sh"]

RUN mkdir -p /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& chown -R cassandra:cassandra /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& chmod 777 /var/lib/cassandra "$CASSANDRA_CONFIG" \
	&& mkdir -p "/$DISTRO_NAME/logs" \
	&& mkdir -p /var/log/cassandra \
	&& chown -R cassandra:cassandra "/$DISTRO_NAME" \
	&& ln -s /$DISTRO_NAME /apache-cassandra 

RUN sed -i 's/^start_rpc.*$/start_rpc: true/' $CASSANDRA_CONFIG/cassandra.yaml 

ENV PATH /apache-cassandra/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
VOLUME /var/lib/cassandra

# 7000: intra-node communication
# 7001: TLS intra-node communication
# 7199: JMX
# 9042: CQL
# 9160: thrift service
EXPOSE 7000 7001 7199 9042 9160

CMD ["cassandra", "-f"]

RUN [ "cross-build-end" ] 
