FROM dockerfile/java:oracle-java7

ENV ES_PKG_NAME elasticsearch-1.4.1

# Install ElasticSearch.
RUN \
  cd / && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz && \
  tar xvzf $ES_PKG_NAME.tar.gz && \
  rm -f $ES_PKG_NAME.tar.gz && \
  mv /$ES_PKG_NAME /elasticsearch

RUN cd /elasticsearch && bin/plugin install elasticsearch/elasticsearch-cloud-aws/2.4.1

VOLUME ["/data"]

ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml
ADD analysis /elasticsearch/config/analysis
ADD hunspell /elasticsearch/config/hunspell

WORKDIR /data

CMD ["/elasticsearch/bin/elasticsearch"]

EXPOSE 9200
EXPOSE 9300
