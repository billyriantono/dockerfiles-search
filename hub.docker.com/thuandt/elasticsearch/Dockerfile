FROM quay.io/pires/docker-elasticsearch:2.3.2

MAINTAINER thuandt26@gmail.com

# Override elasticsearch.yml config, otherwise plug-in install will fail
COPY do_not_use.yml /elasticsearch/config/elasticsearch.yml

# Install Elasticsearch plug-ins
RUN /elasticsearch/bin/plugin install delete-by-query --verbose

# Override elasticsearch.yml config, otherwise plug-in install will fail
COPY elasticsearch.yml /elasticsearch/config/elasticsearch.yml
