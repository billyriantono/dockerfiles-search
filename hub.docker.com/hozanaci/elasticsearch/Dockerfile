FROM docker.elastic.co/elasticsearch/elasticsearch:6.6.0

RUN echo "discovery.type: single-node" >> /usr/share/elasticsearch/config/elasticsearch.yml
RUN bin/elasticsearch-plugin install analysis-icu
