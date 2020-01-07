
FROM dockerfile/java:oracle-java7

RUN \
  cd /tmp && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.4.0.Beta1.tar.gz && \
  tar xvzf elasticsearch-1.4.0.Beta1.tar.gz && \
  rm -f elasticsearch-1.4.0.Beta1.tar.gz && \
  mv /tmp/elasticsearch-1.4.0.Beta1 /elasticsearch

WORKDIR /elasticsearch

CMD ["/elasticsearch/bin/elasticsearch"]

EXPOSE 9200
EXPOSE 9300