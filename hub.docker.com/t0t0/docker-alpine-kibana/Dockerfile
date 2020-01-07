# Docker image to run Kibana on nginx
FROM alpine:3.3
MAINTAINER Tomas Vercautter & Toon Lamberigts

ENV KIBANA_VERSION=4.5.0
ENV NODEJS_ALPINE_VERSION=4.3.0-r0

RUN mkdir /opt && \
  wget -q http://download.elastic.co/kibana/kibana/kibana-${KIBANA_VERSION}-linux-x64.tar.gz -O /tmp/kibana.tar.gz && \
  gunzip /tmp/kibana.tar.gz && \
  cd /opt && \
  tar xf /tmp/kibana.tar && \
  rm /tmp/kibana.tar && \
  rm -rf /opt/kibana-${KIBANA_VERSION}-linux-x64/node && \
  ln -s /opt/kibana-${KIBANA_VERSION}-linux-x64/bin/kibana /usr/bin/kibana 

RUN apk --update add nodejs=$NODEJS_ALPINE_VERSION && \
  mkdir -p /opt/kibana-${KIBANA_VERSION}-linux-x64/node/bin && \
  ln -s /usr/bin/node /opt/kibana-${KIBANA_VERSION}-linux-x64/node/bin/node && \
  rm -rf /var/tmp/* /Var/cache/apk/*

# Start kibana, elasticsearch instance can be overridden
EXPOSE 5601

ENTRYPOINT ["kibana","-e"]