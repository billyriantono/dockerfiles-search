# Logstash 6.6.1

# This image re-bundles the Docker image from the upstream provider, Elastic.
FROM docker.elastic.co/logstash/logstash:6.6.1
RUN rm -f /usr/share/logstash/pipeline/logstash.conf
# The upstream image was built by:
#   https://github.com/elastic/logstash-docker/tree/6.6.1

# For a full list of supported images and tags visit https://www.docker.elastic.co

# For Logstash documentation visit https://www.elastic.co/guide/en/logstash/current/docker.html

# See https://github.com/docker-library/official-images/pull/5039 for more details.

RUN  curl http://central.maven.org/maven2/mysql/mysql-connector-java/8.0.13/mysql-connector-java-8.0.13.jar --output ./lib/mysql-connector-java.jar
RUN chmod 4755 ./lib/mysql-connector-java.jar