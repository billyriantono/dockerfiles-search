FROM brainloop/docker-elasticsearch-kubernetes:7.1.0.1

# Override config, otherwise plug-in install will fail
ADD config /elasticsearch/config

# Set environment
ENV DISCOVERY_SERVICE elasticsearch-discovery

# Kubernetes requires swap is turned off, so memory lock is redundant
ENV MEMORY_LOCK false
RUN rm -rf /elasticsearch/plugins/x-pack/x-pack-ml
