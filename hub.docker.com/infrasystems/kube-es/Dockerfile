FROM alpine:3.5

#java install
ENV JAVA_HOME=/usr/lib/jvm/default-jvm/jre
RUN apk upgrade --update-cache; \
    apk add openjdk8-jre;  \
    rm -rf /tmp/* /var/cache/apk/*

#es install
ENV VERSION 2.4.1
RUN apk add --update bash curl ca-certificates sudo util-linux && \
  ( curl -Lskj https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$VERSION/elasticsearch-$VERSION.tar.gz | \
  gunzip -c - | tar xf - ) && \
  mv /elasticsearch-$VERSION /elasticsearch && \
  rm -rf $(find /elasticsearch | egrep "(\.(exe|bat)$)") &&  \
  apk del curl

# Volume for Elasticsearch data
VOLUME ["/data"]

# Copy configuration
COPY config /elasticsearch/config

# Copy run script
COPY run.sh /

# Set environment variables defaults
ENV ES_JAVA_OPTS "-Xms512m -Xmx512m"
ENV CLUSTER_NAME elasticsearch-default
ENV NODE_MASTER true
ENV NODE_DATA true
ENV NODE_INGEST true
ENV HTTP_ENABLE true
ENV NETWORK_HOST 0.0.0.0
ENV HTTP_CORS_ENABLE true
ENV HTTP_CORS_ALLOW_ORIGIN *
ENV NUMBER_OF_MASTERS 1
ENV NUMBER_OF_SHARDS 1
ENV NUMBER_OF_REPLICAS 0
ENV MAX_LOCAL_STORAGE_NODES 1
ENV NAMESPACE default
ENV DISCOVERY_SERVICE elasticsearch-discovery

# Override elasticsearch.yml config, otherwise plug-in install will fail
ADD do_not_use.yml /elasticsearch/config/elasticsearch.yml
# Install Elasticsearch plug-ins
RUN /elasticsearch/bin/plugin install io.fabric8/elasticsearch-cloud-kubernetes/$VERSION --verbose
#RUN /elasticsearch/bin/plugin install analysis-phonetic
#RUN /elasticsearch/bin/plugin install mobz/elasticsearch-head
#RUN /elasticsearch/bin/plugin install lmenezes/elasticsearch-kopf
# Override elasticsearch.yml config, otherwise plug-in install will fail
ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml

EXPOSE 9200 9300

CMD ["/run.sh"]
