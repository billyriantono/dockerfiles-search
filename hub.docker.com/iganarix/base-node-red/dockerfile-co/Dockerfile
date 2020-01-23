FROM openjdk:jre-alpine

LABEL maintainer "erwin <eluz@elektra.com.mx>"

ARG ek_version=6.3.1

RUN apk add --quiet --no-progress --no-cache nodejs wget \
 && adduser -D elasticsearch

USER elasticsearch

WORKDIR /home/elasticsearch

ENV ES_TMPDIR=/home/elasticsearch/elasticsearch.tmp

RUN wget -q -O - https://artifacts.elastic.co/downloads/logstash/logstash-${ek_version}.tar.gz \
 |  tar -zx \
 && mv logstash-${ek_version} logstash \
 && mkdir -p ${ES_TMPDIR} \
 && chmod -R 777 /home/elasticsearch \
 && chown -R elasticsearch:elasticsearch /home/elasticsearch
 
COPY pipeline.conf /home/elasticsearch/pipeline.conf

CMD sh logstash/bin/logstash --http.host 172.30.85.159 -f /home/elasticsearch/pipeline.conf

EXPOSE 8888