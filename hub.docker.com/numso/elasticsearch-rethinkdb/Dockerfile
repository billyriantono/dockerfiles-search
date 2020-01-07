#
# ElasticSearch Dockerfile with RethinkDB river
#
# https://github.com/numso/dockerfile-elasticsearch-rethinkdb
#

# Pull base image.
FROM dockerfile/java:oracle-java8

ENV ES_PKG_NAME elasticsearch-1.3.0

# Install ElasticSearch.
RUN \
  cd / && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz && \
  tar xvzf $ES_PKG_NAME.tar.gz && \
  rm -f $ES_PKG_NAME.tar.gz && \
  mv /$ES_PKG_NAME /elasticsearch

# Install head
RUN \
  cd /elasticsearch && \
  bin/plugin -i mobz/elasticsearch-head

# Install RethinkDB River
RUN \
  cd /elasticsearch && \
  bin/plugin -i river-rethinkdb --url http://goo.gl/JmMwTf

# Define default command.
CMD ["/elasticsearch/bin/elasticsearch"]

# Expose ports.
#   - 9200: HTTP
#   - 9300: transport
EXPOSE 9200
EXPOSE 9300
