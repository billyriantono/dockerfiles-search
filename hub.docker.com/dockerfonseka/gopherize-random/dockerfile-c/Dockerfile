# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Elasticsearch Image Container

FROM dockerbase/service-java8


# Run dockerbase script
ADD     elasticsearch.sh /dockerbase/
RUN     /dockerbase/elasticsearch.sh

ENV     ELASTICSEARCH_HOME /usr/local/elasticsearch
ENV     PATH $PATH:$ELASTICSEARCH_HOME/bin

# Add elasticsearch into runit
ADD     build/runit/elasticsearch /etc/service/elasticsearch/run

EXPOSE  9200
