FROM otasys/java:1.8.0_66

WORKDIR /opt


###############################################################################
#                                INSTALLATION
###############################################################################

RUN apt-get -q update \
 && apt-get install -yq curl supervisor \
 && apt-get clean

## install Elasticsearch
ENV ES_VERSION 2.3.3
ENV ES_HOME /opt/elasticsearch
ENV ES_PACKAGE elasticsearch-${ES_VERSION}.tar.gz
RUN mkdir ${ES_HOME} \
 && curl -fOL https://download.elasticsearch.org/elasticsearch/elasticsearch/${ES_PACKAGE} \
 && tar xzf ${ES_PACKAGE} -C ${ES_HOME} --strip-components=1 \
 && rm -f ${ES_PACKAGE}

## install Logstash
# https://download.elasticsearch.org/logstash/logstash/
ENV LOGSTASH_VERSION 2.3.2
ENV LOGSTASH_HOME /opt/logstash
ENV LOGSTASH_PACKAGE logstash-${LOGSTASH_VERSION}.tar.gz
RUN mkdir ${LOGSTASH_HOME} \
 && curl -fOL https://download.elastic.co/logstash/logstash/${LOGSTASH_PACKAGE} \
 && tar xzf ${LOGSTASH_PACKAGE} -C ${LOGSTASH_HOME} --strip-components=1 \
 && rm -f ${LOGSTASH_PACKAGE}

## install Kibana
ENV KIBANA_VERSION 4.5.1
ENV KIBANA_HOME /opt/kibana
ENV KIBANA_PACKAGE kibana-${KIBANA_VERSION}-linux-x64.tar.gz
RUN mkdir ${KIBANA_HOME} \
 && curl -fOL https://download.elastic.co/kibana/kibana/${KIBANA_PACKAGE} \
 && tar xzf ${KIBANA_PACKAGE} -C ${KIBANA_HOME} --strip-components=1 \
 && rm -f ${KIBANA_PACKAGE}

## Install Redis
ENV REDIS_HOME /opt/redis
RUN apt-get -yq install redis-server \
 && apt-get clean \
 && mkdir ${REDIS_HOME} \
 && mkdir ${REDIS_HOME}/logs

## config Logstash
ADD ./logstash/logstash-indexer.conf /etc/logstash/conf.d/logstash-indexer.conf

## config Redis
ADD ./redis/redis.conf /opt/redis/redis.conf

ADD ./supervisor/elasticsearch.conf /etc/supervisor/conf.d/
ADD ./supervisor/logstash.conf /etc/supervisor/conf.d/
ADD ./supervisor/kibana.conf /etc/supervisor/conf.d/
ADD ./supervisor/redis.conf /etc/supervisor/conf.d/

# Remove unwanted applications & Clean Installations
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN useradd --shell /bin/bash -u 1024 -o -c "" -m miku
RUN chown -R 1024:1024 /opt/* /var/log/supervisor

#USER miku

# Exposing Redis Server Port, Kibana Port and SYSLOG Port
EXPOSE 6379
EXPOSE 9292
EXPOSE 9200

# Start supervisor
CMD /usr/bin/supervisord -n -c /etc/supervisor/supervisord.conf

