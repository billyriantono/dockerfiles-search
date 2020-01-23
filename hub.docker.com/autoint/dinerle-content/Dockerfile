FROM elasticsearch:1.5

RUN plugin install elasticsearch/elasticsearch-cloud-aws/2.5.1
RUN plugin install lmenezes/elasticsearch-kopf/1.0

COPY config/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml

EXPOSE 9200 9300

CMD ["elasticsearch"]
