FROM pires/elasticsearch:base

MAINTAINER idoesh1@gmail.com

# Override elasticsearch.yml config, otherwise plug-in install will fail
# ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml
# ADD logging.yml /elasticsearch/config/logging.yml

# Install Kubernetes discovery plug-in
# RUN /elasticsearch/bin/plugin --install fabric8io/elasticsearch-cloud-kubernetes/1.1.1 --verbose

# Install custom plugins
ENV ES_PLUGINS ""
COPY entrypoint.sh /elasticsearch/entrypoint.sh
CMD ["/elasticsearch/entrypoint.sh"]
