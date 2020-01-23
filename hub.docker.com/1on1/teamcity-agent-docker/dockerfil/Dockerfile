FROM quay.io/pires/docker-jre:8u112_1
#RUN /elasticsearch/bin/plugin -i io.fabric8/elasticsearch-cloud-kubernetes
# Export HTTP & Transport
EXPOSE 9200 9300

ENV VERSION 2.4.4

# Install Elasticsearch.
RUN apk add --update bash curl ca-certificates sudo && \
  ( curl -Lskj https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.4.4/elasticsearch-2.4.4.tar.gz | \
  gunzip -c - | tar xf - ) && \
  mv /elasticsearch-$VERSION /elasticsearch && \
  rm -rf $(find /elasticsearch | egrep "(\.(exe|bat)$)") && \
  apk del curl

RUN  /elasticsearch/bin/plugin install io.fabric8/elasticsearch-cloud-kubernetes/2.4.4 --verbose
RUN  /elasticsearch/bin/plugin install lmenezes/elasticsearch-kopf --verbose 
RUN  /elasticsearch/bin/plugin install royrusso/elasticsearch-HQ
RUN mkdir -p /elasticsearch/logs && chmod -R 777 /elasticsearch
ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml
COPY run.sh /
# Set environment variables defaults
#ENV ES_JAVA_OPTS "-Xms512m -Xmx512m"
ENV ES_HEAP_SIZE 5G
ENV CLUSTER_NAME elasticsearch-default
ENV NODE_MASTER true
ENV NODE_DATA true
ENV NODE_INGEST true
ENV HTTP_ENABLE true
ENV NETWORK_HOST _site_
ENV HTTP_CORS_ENABLE true
ENV HTTP_CORS_ALLOW_ORIGIN *
ENV NUMBER_OF_MASTERS 1
ENV NUMBER_OF_SHARDS 1
ENV NUMBER_OF_REPLICAS 0
ENV MAX_LOCAL_STORAGE_NODES 1
CMD ["/run.sh"]

