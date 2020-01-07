FROM elasticsearch:2.2.0
MAINTAINER erik.aulin@zook.ai

ENV ES_HEAP_SIZE 2g

RUN /usr/share/elasticsearch/bin/plugin install lmenezes/elasticsearch-kopf/v2.1.1
RUN /usr/share/elasticsearch/bin/plugin install https://github.com/jprante/elasticsearch-langdetect/releases/download/2.2.0.1/elasticsearch-langdetect-2.2.0.1-plugin.zip

EXPOSE 9200
EXPOSE 9300
