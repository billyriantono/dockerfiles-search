FROM ubuntu:latest

MAINTAINER dchambon <damien.chambon.pro@gmail.com>

RUN apt-get update -q

RUN apt-get install -yq wget default-jre-headless

ENV ES_VERSION 1.7.2

RUN cd /tmp && \
    wget -nv https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-${ES_VERSION}.tar.gz && \
    tar zxf elasticsearch-${ES_VERSION}.tar.gz && \
    rm -f elasticsearch-${ES_VERSION}.tar.gz && \
    mv /tmp/elasticsearch-${ES_VERSION} /elasticsearch

RUN /elasticsearch/bin/plugin -install mobz/elasticsearch-head
RUN /elasticsearch/bin/plugin -install lmenezes/elasticsearch-kopf

CMD /elasticsearch/bin/elasticsearch -Des.http.cors.enabled=true -Des.logger.level=OFF

EXPOSE 9200
