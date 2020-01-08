FROM podbox/java8

ENV ELASTICSEARCH_VERSION 2.3.0
RUN (curl -L https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$ELASTICSEARCH_VERSION/elasticsearch-$ELASTICSEARCH_VERSION.tar.gz | gunzip -c | tar x) \
 && mv elasticsearch-$ELASTICSEARCH_VERSION /elasticsearch

RUN sed -i 's/# network.host: 192.168.0.1/network.host: 0.0.0.0/' /elasticsearch/config/elasticsearch.yml

RUN useradd -m elasticsearch \
 && chown -R elasticsearch:elasticsearch /elasticsearch

USER elasticsearch
EXPOSE 9200 9300
CMD ["/elasticsearch/bin/elasticsearch"]
