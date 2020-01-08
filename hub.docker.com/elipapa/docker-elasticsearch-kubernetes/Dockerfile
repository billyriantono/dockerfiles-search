FROM quay.io/pires/docker-elasticsearch:2.4.1

MAINTAINER pjpires@gmail.com

# Override elasticsearch.yml config, otherwise plug-in install will fail
ADD do_not_use.yml /elasticsearch/config/elasticsearch.yml

# Install Elasticsearch plug-ins
RUN /elasticsearch/bin/plugin install io.fabric8/elasticsearch-cloud-kubernetes/2.4.1 --verbose
RUN /elasticsearch/bin/plugin install --batch license --timeout 5m
RUN /elasticsearch/bin/plugin install --batch marvel-agent --timeout 5m
RUN /elasticsearch/bin/plugin install --batch lang-python
RUN /elasticsearch/bin/plugin install lmenezes/elasticsearch-kopf/v2.1.2
RUN /elasticsearch/bin/plugin install --batch cloud-aws --timeout 5m

# Override elasticsearch.yml config, otherwise plug-in install will fail
ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml

# Set environment
ENV NAMESPACE default
ENV DISCOVERY_SERVICE elasticsearch-discovery
