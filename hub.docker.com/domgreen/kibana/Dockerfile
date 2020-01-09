FROM ubuntu:14.04
MAINTAINER Dominic Green <dom@huddle.com>

ADD https://download.elasticsearch.org/kibana/kibana/kibana-4.0.1-linux-x64.tar.gz /tmp/kibana.tgz
RUN tar -xvzf /tmp/kibana.tgz -C /tmp && \
    mkdir /opt/kibana && \
    mv /tmp/kibana*/* /opt/kibana && \
    rm -rf /tmp/*

EXPOSE 5601

WORKDIR /opt/kibana/bin

CMD ./kibana --elasticsearch "http://$ELASTICSEARCH_PORT_9200_TCP_ADDR:9200"

