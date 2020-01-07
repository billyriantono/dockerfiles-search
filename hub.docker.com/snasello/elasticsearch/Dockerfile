# Elasticsearch
#
# VERSION 0.0.1
#

FROM snasello/java:debian-java8u25

MAINTAINER Samuel Nasello <samuel.nasello@elosi.com>

ENV ES_VERSION 1.3.5
ENV ES_HOME /elasticsearch

# Install ElasticSearch.
RUN curl -kLOH "" http://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-${ES_VERSION}.tar.gz \
	&& tar xfz /elasticsearch-${ES_VERSION}.tar.gz -C / \
	&& rm -f /elasticsearch-${ES_VERSION}.tar.gz \
	&& ln -s  /elasticsearch-${ES_VERSION} ${ES_HOME}

# Define mountable directories.
VOLUME ["/elasticsearch/data","/elasticsearch/logs","/elasticsearch/plugins","/elasticsearch/work"]

# Define working directory.
WORKDIR /elasticsearch

# Define default command.
CMD ["/elasticsearch/bin/elasticsearch"]

# Expose ports.
#   - 9200: HTTP
#   - 9300: transport
EXPOSE 9200
EXPOSE 9300
