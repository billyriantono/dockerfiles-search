FROM alpine:3.10

ARG ek_version=7.5.1

RUN apk add --quiet --no-progress --no-cache openjdk11-jre \
 && apk add --quiet --no-progress --no-cache nodejs \
 && adduser -D elasticsearch
 
USER elasticsearch
 
WORKDIR /home/elasticsearch
 
 ENV ES_DATADIR=/home/elasticsearch/elasticsearch/data \
    JAVA_HOME=/usr/lib/jvm/java-11-openjdk
    

RUN wget -q -O - https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-oss-${ek_version}-no-jdk-linux-x86_64.tar.gz \
 |  tar -zx \
 && mv elasticsearch-${ek_version} elasticsearch \
 && mkdir -p ${ES_DATADIR} \
 && wget -q -O - https://artifacts.elastic.co/downloads/kibana/kibana-oss-${ek_version}-linux-x86_64.tar.gz \
 |  tar -zx \
 && mv kibana-${ek_version}-linux-x86_64 kibana \
 && rm -f kibana/node/bin/node \
 && ln -s $(which node) kibana/node/bin/node
CMD elasticsearch/bin/elasticsearch-plugin install x-pack & kibana/bin/kibana-plugin install x-pack
CMD sh elasticsearch/bin/elasticsearch -E http.host=0.0.0.0 --quiet & kibana/bin/kibana --host 0.0.0.0 -Q

EXPOSE 9200 5601
