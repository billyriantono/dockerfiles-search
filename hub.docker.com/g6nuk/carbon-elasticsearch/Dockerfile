FROM quay.io/pires/docker-elasticsearch:5.5.2
ADD config /elasticsearch/config
ARG NODE_NAME=random
ENV DISCOVERY_SERVICE elasticsearch-discovery
ENV MEMORY_LOCK false
RUN elasticsearch-plugin install --batch repository-s3
