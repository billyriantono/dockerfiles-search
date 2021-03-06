# based on https://github.com/clairton/elasticsearch/tree/master/5

FROM openjdk:8-jre-alpine

# ensure elasticsearch user exists
RUN addgroup -S elasticsearch && adduser -S -G elasticsearch elasticsearch

# grab su-exec for easy step-down from root
# and bash for "bin/elasticsearch" among others
RUN apk add --no-cache 'su-exec>=0.2' bash

# https://artifacts.elastic.co/GPG-KEY-elasticsearch
ENV GPG_KEY 46095ACC8548582C1A2699A9D27D666CD88E42B4

WORKDIR /usr/share/elasticsearch
ENV PATH /usr/share/elasticsearch/bin:$PATH

ENV ELASTICSEARCH_VERSION 6.2.3
ENV ELASTICSEARCH_TARBALL="https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${ELASTICSEARCH_VERSION}.tar.gz"

RUN set -ex; \
	\
	apk add --no-cache --virtual .fetch-deps \
		ca-certificates \
		gnupg \
		openssl \
		tar

RUN	wget -O elasticsearch.tar.gz "$ELASTICSEARCH_TARBALL"; \
	tar -xf elasticsearch.tar.gz --strip-components=1; \
	rm elasticsearch.tar.gz

RUN	apk del .fetch-deps;

RUN mkdir -p ./plugins; \
	for path in \
		./data \
		./logs \
		./config \
		./config/scripts \
	; do \
		mkdir -p "$path"; \
		chown -R elasticsearch:elasticsearch "$path"; \
	done;

ENV NODE_NAME ''
ENV ES_TMPDIR '/tmp'

# we shouldn't need much RAM to test --version (default is 2gb, which gets Jenkins in trouble sometimes)
RUN	export ES_JAVA_OPTS='-Xms32m -Xmx32m';

RUN	elasticsearch --version

COPY config ./config

VOLUME /usr/share/elasticsearch/data

COPY docker-entrypoint.sh /

ENV LANG=pt_BR.UTF-8
ENV LANGUAGE=pt_BR.UTF-8
ENV LC_CTYPE=pt_BR.UTF-8
ENV LC_ALL=pt_BR.UTF-8
RUN ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]

# build with docker build . --tag artemis_elasticsearch
