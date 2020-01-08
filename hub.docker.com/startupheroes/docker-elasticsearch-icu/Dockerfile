FROM docker.elastic.co/elasticsearch/elasticsearch:7.1.0

COPY elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml
COPY logging.yml /usr/share/elasticsearch/config/logging.yml

RUN bin/elasticsearch-plugin install analysis-icu
