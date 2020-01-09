FROM openjdk:jre-alpine

LABEL maintainer "erwin <eluz@elektra.com.mx>"

ARG ek_version=6.3.1

RUN apk add --quiet --no-progress --no-cache nodejs wget \
 && adduser -D elasticsearch

USER elasticsearch

WORKDIR /home/elasticsearch

ENV ES_TMPDIR=/home/elasticsearch/elasticsearch.tmp

RUN wget -q -O - https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-oss-${ek_version}.tar.gz \
 |  tar -zx \
 && mv elasticsearch-${ek_version} elasticsearch \
 && mkdir -p ${ES_TMPDIR} \
 && wget -q -O - https://artifacts.elastic.co/downloads/kibana/kibana-oss-${ek_version}-linux-x86_64.tar.gz \
 |  tar -zx \
 && mv kibana-${ek_version}-linux-x86_64 kibana \
 && rm -f kibana/node/bin/node kibana/node/bin/npm \
 && ln -s $(which node) kibana/node/bin/node \
 && ln -s $(which npm) kibana/node/bin/npm \
 && wget -q -O - https://artifacts.elastic.co/downloads/logstash/logstash-${ek_version}.tar.gz \
 |  tar -zx \
 && mv logstash-${ek_version} logstash \
 && chmod -R 777 /home/elasticsearch \
 && chown -R elasticsearch:elasticsearch /home/elasticsearch

COPY pipeline.conf /home/elasticsearch/pipeline3.conf

CMD sh elasticsearch/bin/elasticsearch -E http.host=0.0.0.0 --quiet & kibana/bin/kibana --host 0.0.0.0 -Q & sh logstash/bin/logstash -f /home/elasticsearch/pipeline3.conf

EXPOSE 9200 5601 8888