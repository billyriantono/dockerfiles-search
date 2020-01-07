FROM anapsix/alpine-java:8
MAINTAINER mklimuk, https://github.com/mklimuk/docker-alpine

# Set environment variables
ENV ELASTIC_VERSION 2.3.2
ENV ELASTIC_HOME /opt/elasticsearch
ENV ELASTIC_DATA /var/lib/elasticsearch

# Download Elasticsearch
RUN apk update && apk add openssl \
    && wget -O /tmp/elasticsearch-$ELASTIC_VERSION.tar.gz https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-$ELASTIC_VERSION.tar.gz \
    && tar -xvzf /tmp/elasticsearch-$ELASTIC_VERSION.tar.gz -C /opt/ \
    && ln -s /opt/elasticsearch-$ELASTIC_VERSION $ELASTIC_HOME \
    && rm -rf /tmp/*.tar.gz /var/cache/apk/* \
    && mkdir $ELASTIC_DATA && chown -R nobody:nobody $ELASTIC_DATA \
    && chown -R nobody:nobody $ELASTIC_HOME /opt/elasticsearch-$ELASTIC_VERSION

# Add files
COPY config/elasticsearch.yml $ELASTIC_HOME/config/elasticsearch.yml
COPY scripts/run.sh /scripts/run.sh

# Specify Volume
VOLUME [$ELASTIC_DATA]

# Exposes
EXPOSE 9200
EXPOSE 9300

USER nobody

# CMD
ENTRYPOINT ["/scripts/run.sh"]
