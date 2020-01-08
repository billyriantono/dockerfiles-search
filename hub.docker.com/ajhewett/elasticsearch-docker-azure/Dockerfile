FROM docker.elastic.co/elasticsearch/elasticsearch:5.2.0

USER elasticsearch

# Install azure plugin
RUN eval ${ES_JAVA_OPTS:-} elasticsearch-plugin install repository-azure

COPY bin/es-swarm-docker bin/es-swarm-docker

USER root
RUN chown elasticsearch.elasticsearch bin/es-swarm-docker && \
    chmod 0750 bin/es-swarm-docker

USER elasticsearch
CMD ["/bin/bash", "bin/es-swarm-docker", "bin/es-docker"]

EXPOSE 9200 9300

