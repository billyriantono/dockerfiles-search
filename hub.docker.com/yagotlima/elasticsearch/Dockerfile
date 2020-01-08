FROM openjdk:8

ARG ES_VERSION=1.7.1

WORKDIR /opt

RUN wget https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-$ES_VERSION.zip && \
    wget https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-$ES_VERSION.zip.sha1.txt && \
    sha1sum -c elasticsearch-$ES_VERSION.zip.sha1.txt && \
    unzip elasticsearch-$ES_VERSION.zip && \
    mv elasticsearch-$ES_VERSION elasticsearch

WORKDIR /opt/elasticsearch

VOLUME /opt/elasticsearch/data

ENV JAVA_OPTS="-server"

ENTRYPOINT [ "/opt/elasticsearch/bin/elasticsearch" ]
