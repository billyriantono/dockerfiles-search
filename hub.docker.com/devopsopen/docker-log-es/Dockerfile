# 
# Elasticsearch Docker Image for Open DevOps Pipeline 
# 
# VERSION : 1.0 
# 
FROM alpine

MAINTAINER Open DevOps Team <open.devops@gmail.com>

ENV REFRESHED_AT 2016-09-01

ENV ES_VERSION=2.3.5

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk/jre
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u92
ENV JAVA_ALPINE_VERSION 8.92.14-r1

RUN set -x \
	&& apk add --no-cache \
		openjdk8-jre="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]

ADD https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$ES_VERSION/elasticsearch-$ES_VERSION.tar.gz /tmp/es.tgz
RUN cd /usr/share && \
  tar xf /tmp/es.tgz && \
  rm /tmp/es.tgz

ADD start /start

EXPOSE 9200 9300

ENV ES_HOME=/usr/share/elasticsearch-$ES_VERSION \
    OPTS=-Dnetwork.host=_non_loopback_ \
    DEFAULT_ES_USER=elasticsearch

RUN adduser -S -s /bin/sh $DEFAULT_ES_USER

VOLUME ["/data","/conf"]

WORKDIR $ES_HOME

CMD ["/start"]
