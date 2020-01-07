# Pull base image.
FROM elasticsearch:2.4.1

RUN echo "index.number_of_replicas: 0" >> /usr/share/elasticsearch/config/elasticsearch.yml

# Install HEAD / KOPF plugin
RUN \
  cd /usr/share/elasticsearch && \
  bin/plugin install mobz/elasticsearch-head && \
  bin/plugin install lmenezes/elasticsearch-kopf
