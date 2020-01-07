FROM openjdk:jre-alpine
MAINTAINER Sergey Bovyrin <sbovyrin@gmail.com> (https://sbovyrin.com)

ENV ES_VERSION=5.4.2
ENV XMS=-Xms128m
ENV XMX=-Xmx128m

RUN apk add --no-cache wget && adduser -D elasticsearch

USER elasticsearch

WORKDIR /home/elasticsearch

RUN wget -q -O - https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${ES_VERSION}.tar.gz \
|  tar -zx \
&& mv elasticsearch-${ES_VERSION} elasticsearch \
&& sed -i "s/-Xms2g/${XMS}/" elasticsearch/config/jvm.options \
&& sed -i "s/-Xmx2g/${XMX}/" elasticsearch/config/jvm.options

USER root

RUN apk del --purge wget && rm -rf /tmp/* /var/cache/apk/*

USER elasticsearch

CMD sh elasticsearch/bin/elasticsearch -E http.host=0.0.0.0 --quiet

EXPOSE 9200
