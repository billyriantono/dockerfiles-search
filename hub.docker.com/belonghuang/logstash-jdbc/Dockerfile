# Logstash 6.6.1

# This image re-bundles the Docker image from the upstream provider, Elastic.
FROM docker.elastic.co/logstash/logstash:6.6.1@sha256:4ab088b1c9b3e98c9e7f1c814de628046047d0b43d03b87adce4f4e91fa6d308

# The upstream image was built by:
#   https://github.com/elastic/logstash-docker/tree/6.6.1

# For a full list of supported images and tags visit https://www.docker.elastic.co
RUN yes|./bin/logstash-plugin install logstash-input-jdbc
# For Logstash documentation visit https://www.elastic.co/guide/en/logstash/current/docker.html

# See https://github.com/docker-library/official-images/pull/5039 for more details.
