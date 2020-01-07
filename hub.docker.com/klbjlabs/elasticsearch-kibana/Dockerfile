FROM openjdk:jre-alpine

MAINTAINER Jia Tian <klbjlabs@gmail.com>

ENV ES_VERSION=6.3.1 \
    KIBANA_VERSION=6.3.1

RUN apk add --quiet --no-progress --no-cache nodejs wget net-tools vim bash curl su-exec \
    && adduser -D elasticsearch

COPY entrypoint.sh /entrypoint.sh

USER elasticsearch

WORKDIR /home/elasticsearch

RUN wget -q -O - https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${ES_VERSION}.tar.gz \
    |  tar -zx \
    && mv elasticsearch-${ES_VERSION} elasticsearch \
    && wget -q -O - https://artifacts.elastic.co/downloads/kibana/kibana-${KIBANA_VERSION}-linux-x86_64.tar.gz \
    |  tar -zx \
    && mv kibana-${KIBANA_VERSION}-linux-x86_64 kibana \
    && rm -f kibana/node/bin/node kibana/node/bin/npm \
    && ln -s $(which node) kibana/node/bin/node \
    && ln -s $(which npm) kibana/node/bin/npm

USER root
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 9200 5601
