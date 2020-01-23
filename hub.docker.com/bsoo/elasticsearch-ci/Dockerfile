FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.1.1

RUN bin/elasticsearch-plugin install analysis-kuromoji

ADD ./elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml

EXPOSE 9200
