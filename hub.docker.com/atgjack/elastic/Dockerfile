FROM atgjack/java 
MAINTAINER atgJack, https://github.com/atgJack/docker-alpine

# Set environment variables
ENV ES_VERSION 2.4.0
ENV PKG_NAME elasticsearch
ENV ES_PKG $PKG_NAME-$ES_VERSION
ENV ES_URL https://download.elastic.co/$PKG_NAME/$PKG_NAME/$ES_PKG.tar.gz
ENV ES_HOME /usr/$PKG_NAME
ENV PATH ${PATH}:${ES_HOME}/bin
ENV ES_USER elasticsearch

# Download Elasticsearch
RUN apk update \
    && adduser -S $ES_USER \
    && apk add curl openssl \
    && apk --update add tar \
    && mkdir -p $ES_HOME \  
    && wget -O /tmp/$ES_PKG.tar.gz $ES_URL \
    && tar -xzf /tmp/$ES_PKG.tar.gz --strip-components=1 -C $ES_HOME \
    && rm -rf /tmp/*.tar.gz /var/cache/apk/* \
    && mkdir /var/lib/elasticsearch 

# Add files and set permissions
COPY config /usr/elasticsearch/config
RUN chown $ES_USER /var/lib/elasticsearch \
    && chown $ES_USER -R $ES_HOME

# Specify Volume
VOLUME ["/var/lib/elasticsearch"]

# Exposes
EXPOSE 9200 9300

USER elasticsearch

# CMD
ENTRYPOINT ["elasticsearch"]
