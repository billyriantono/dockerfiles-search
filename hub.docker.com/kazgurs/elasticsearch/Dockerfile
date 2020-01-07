FROM docker.elastic.co/elasticsearch/elasticsearch:6.7.1

RUN echo 'http.host: 0.0.0.0' >> /usr/share/elasticsearch/config/elasticsearch.yml \
    && echo 'http.cors.enabled: true' >> /usr/share/elasticsearch/config/elasticsearch.yml \
    && echo 'http.cors.allow-origin: "*"' >> /usr/share/elasticsearch/config/elasticsearch.yml \
    && bin/elasticsearch-plugin install analysis-icu
