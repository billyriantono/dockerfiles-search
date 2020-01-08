FROM java:openjdk-7-jre

WORKDIR /usr/local/elasticsearch

# elasticsearch
RUN curl -L https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-1.4.2.tar.gz \
  | tar -xz --strip-components 1

VOLUME ["/usr/local/elasticsearch/data"]
CMD ["bin/elasticsearch"]
EXPOSE 9200 9300
