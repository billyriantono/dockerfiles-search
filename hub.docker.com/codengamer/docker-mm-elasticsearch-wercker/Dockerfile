FROM docker.elastic.co/elasticsearch/elasticsearch:6.1.0

ENV ES_VERSION 6.1.0 

WORKDIR /usr/share/elasticsearch

COPY config/elasticsearch.yml /usr/share/elasticsearch/config/

CMD ["elasticsearch"]
