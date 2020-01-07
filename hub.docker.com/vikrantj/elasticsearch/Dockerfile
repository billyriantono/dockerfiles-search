FROM vikrantj/java:8u101

MAINTAINER Vikrant Jain <vikrantj.develop@gmail.com>

ARG ES_VERSION=2.3.3
ARG ES_URL=https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-${ES_VERSION}.tar.gz


RUN curl -SL ${ES_URL} -o elasticsearch.tar.gz \
    && tar zxf elasticsearch.tar.gz \
    && rm -rf elasticsearch.tar.gz \
    && mv elasticsearch-${ES_VERSION} elasticsearch

EXPOSE 9300 9200

ENTRYPOINT ["/elasticsearch/bin/elasticsearch","-Des.insecure.allow.root=true"]
