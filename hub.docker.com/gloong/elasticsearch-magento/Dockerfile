FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.11

RUN bin/elasticsearch-plugin remove x-pack --purge \
    && bin/elasticsearch-plugin install analysis-phonetic \
    && bin/elasticsearch-plugin install analysis-icu