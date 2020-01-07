#
# ElasticSearch Dockerfile
#
# https://github.com/dockerfile/elasticsearch
#

# Pull base image.
FROM corvis/java8

# Install ElasticSearch.
RUN \
  cd /tmp && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.7.1.tar.gz && \
  tar xvzf elasticsearch-1.7.1.tar.gz && \
  rm -f elasticsearch-1.7.1.tar.gz && \
  mv /tmp/elasticsearch-1.7.1 /elasticsearch && \
  /elasticsearch/bin/plugin -install lmenezes/elasticsearch-kopf && \
  /elasticsearch/bin/plugin -install royrusso/elasticsearch-HQ

# Define mountable directories.
VOLUME ["/data"]

# Mount elasticsearch.yml config
ADD config/elasticsearch.yml /elasticsearch/config/elasticsearch.yml
ADD bin/init.sh /elasticsearch/bin/init.sh

# Define working directory.
WORKDIR /data

# Define default command.
#CMD ["/elasticsearch/bin/elasticsearch"]
CMD ["/elasticsearch/bin/init.sh"]

# Expose ports.
#   - 9200: HTTP
#   - 9300: transport
EXPOSE 9200
EXPOSE 9300