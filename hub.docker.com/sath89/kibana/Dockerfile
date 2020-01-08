FROM ubuntu:latest

MAINTAINER Maksym Bilenko "sath891@gmail.com"

ENV DEBIAN_FRONTEND noninteractive
ENV KIBANA_VERSION 4.0.2
ENV ELASTICSEARCH_URL http://elasticsearch:9200

RUN apt-get update -q && apt-get install curl -y -q && \
    curl -sLo /tmp/kibana-${KIBANA_VERSION}-linux-x64.tar.gz https://download.elastic.co/kibana/kibana/kibana-${KIBANA_VERSION}-linux-x64.tar.gz && \
    tar xf /tmp/kibana-${KIBANA_VERSION}-linux-x64.tar.gz -C /opt && \
    apt-get clean && rm -rf /tmp/* /var/lib/apt/lists/* /var/tmp/*

CMD /opt/kibana-${KIBANA_VERSION}-linux-x64/bin/kibana -q -e ${ELASTICSEARCH_URL}

EXPOSE 5601/tcp