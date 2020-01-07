FROM srakshit/alpine-base

MAINTAINER Subham Rakshit

ENV ELASTICSEARCH_HOME="/opt/elasticsearch" \
    ELASTICSEARCH_VERSION="1.5.1" \
    PATH=$PATH:$ELASTICSEARCH_HOME/bin

ADD ./elasticsearch-* /opt/

RUN chmod +x /opt/elasticsearch-download.sh \
    && sleep 1 \
    && /opt/elasticsearch-download.sh \
    && rm /opt/elasticsearch-download.sh \
    && ln -s /opt/elasticsearch-$ELASTICSEARCH_VERSION $ELASTICSEARCH_HOME \
    && addgroup elasticsearch \
    && adduser -S -G elasticsearch elasticsearch \
    && chown elasticsearch:elasticsearch -R /opt/elasticsearch* \
    && chmod 754 /opt/elasticsearch*
