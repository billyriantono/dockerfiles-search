FROM anapsix/alpine-java
MAINTAINER atgJack, https://github.com/atgJack/dockerfiles

# Set environment variables
ENV LOGSTASH_VERSION 2.4.0
ENV LOGSTASH_NAME logstash
ENV LOGSTASH_PKG $LOGSTASH_NAME-$LOGSTASH_VERSION
ENV LOGSTASH_URL https://download.elastic.co/$LOGSTASH_NAME/$LOGSTASH_NAME/$LOGSTASH_PKG.tar.gz
ENV LOGSTASH_HOME /usr/$LOGSTASH_NAME
ENV LOGSTASH_CONFIG $LOGSTASH_HOME/etc/logstash.json

ENV PATH ${PATH}:${LOGSTASH_HOME}/bin

# Download Elasticsearch
RUN apk update \
    && apk add curl openssl bash \
    && apk --update add tar \
    && mkdir -p $LOGSTASH_HOME \  
    && curl -L -o /tmp/$LOGSTASH_PKG.tar.gz $LOGSTASH_URL \
    && tar -xzf /tmp/$LOGSTASH_PKG.tar.gz --strip-components=1 -C $LOGSTASH_HOME \
    && rm -rf /tmp/*.tar.gz /var/cache/apk/* \
    && mkdir /etc/logstash \
    && mkdir /scripts \
    && chmod -R 755 /scripts

# Add files and set permissions
ADD config $LOGSTASH_HOME/etc
ADD scripts /scripts

# Exposes
EXPOSE 514 514/udp 8080

# CMD
CMD ["/scripts/run.sh"]
