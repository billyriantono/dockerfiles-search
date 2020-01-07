FROM elasticsearch:latest

COPY config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml

RUN plugin -i elasticsearch/marvel/latest
