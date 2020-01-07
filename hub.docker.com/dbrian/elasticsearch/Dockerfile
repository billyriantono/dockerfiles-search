FROM dockerfile/java:oracle-java8

ENV ES_PKG_NAME elasticsearch-1.2.1

RUN \
  cd / && \
  wget -q https://download.elasticsearch.org/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz -O - | tar zxvf - && \
  mv /$ES_PKG_NAME /elasticsearch && \
  /elasticsearch/bin/plugin -install royrusso/elasticsearch-HQ && \
  /elasticsearch/bin/plugin -install mobz/elasticsearch-head

VOLUME ["/data"]

ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml

CMD ["/elasticsearch/bin/elasticsearch"]

EXPOSE 9200 9300



