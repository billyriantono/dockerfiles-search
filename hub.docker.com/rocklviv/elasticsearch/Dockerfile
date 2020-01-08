FROM rocklviv/alpine-java:8.45.14
MAINTAINER Denis Chekirda <dchekirda@gmail.com>

ENV ELASTICSEARCH_VERSION 2.3.1
ENV USER elastic

RUN apk update && apk upgrade
RUN apk add curl wget

RUN \
  mkdir -p /opt && \
  cd /tmp && \
  wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-$ELASTICSEARCH_VERSION.tar.gz && \
  tar -xzf elasticsearch-$ELASTICSEARCH_VERSION.tar.gz && \
  rm -rf elasticsearch-$ELASTICSEARCH_VERSION.tar.gz && \
  mv elasticsearch-$ELASTICSEARCH_VERSION /opt/elasticsearch && \
  adduser -S ${USER} && \
  chown -R ${USER} /opt && \
  mkdir -p /var/lib/elasticsearch &&\
  chown ${USER} -R /var/lib/elasticsearch

ADD ./elasticsearch.yml /opt/elasticsearch/config/elasticsearch.yml

VOLUME ["/var/lib/elasticsearch"]

EXPOSE 9200
EXPOSE 9300
USER ${USER}

CMD ["/opt/elasticsearch/bin/elasticsearch"]
