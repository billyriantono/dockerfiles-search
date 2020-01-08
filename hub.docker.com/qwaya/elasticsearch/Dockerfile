FROM debian:latest

MAINTAINER qwaya

RUN \
  apt-get update && \
  apt-get install -y wget openjdk-7-jre-headless && \
  cd /tmp && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.3.1.tar.gz && \
  tar xvzf elasticsearch-1.3.1.tar.gz && \
  rm -f elasticsearch-1.3.1.tar.gz && \
  mv /tmp/elasticsearch-1.3.1 /elasticsearch && \
  /elasticsearch/bin/plugin -install elasticsearch/elasticsearch-cloud-aws/2.2.0

ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml

# Define mountable directories.
VOLUME ["/data"]

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["/elasticsearch/bin/elasticsearch"]

# Expose ports.
#   - 9200: HTTP
#   - 9300: transport
EXPOSE 9200
EXPOSE 9300
