# Elasticsearch 6.5.4

# This image re-bundles the Docker image from the upstream provider, Elastic.

FROM docker.elastic.co/elasticsearch/elasticsearch:6.5.4@sha256:5ca85697b6273f63196b44c32311c5a2d1135af9cfd919e5922e49c5045d04b8
ARG VERSION=6.5.4

# do all in one step
RUN cd /usr/share/elasticsearch/plugins/ && \
    wget https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v${VERSION}/elasticsearch-analysis-ik-${VERSION}.zip && \
    wget https://github.com/medcl/elasticsearch-analysis-pinyin/releases/download/v${VERSION}/elasticsearch-analysis-pinyin-${VERSION}.zip && \
    unzip elasticsearch-analysis-ik-${VERSION}.zip -d ik && rm -f elasticsearch-analysis-ik-${VERSION}.zip && \
    unzip elasticsearch-analysis-pinyin-${VERSION}.zip -d pinyin && rm -f elasticsearch-analysis-pinyin-${VERSION}.zip

# The upstream image was built by:
#   https://github.com/elastic/elasticsearch-docker/tree/6.5.4

# For a full list of supported images and tags visit https://www.docker.elastic.co

# For Elasticsearch documentation visit https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

# See https://github.com/docker-library/official-images/pull/4916 for more details.