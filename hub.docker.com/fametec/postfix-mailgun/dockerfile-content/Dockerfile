FROM elasticsearch:5-alpine

# installs plugins necessary for Smile ElasticSuite
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-phonetic \
    && /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu
