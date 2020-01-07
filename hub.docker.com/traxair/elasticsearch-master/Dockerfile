FROM traxair/elasticsearch:latest

RUN /usr/share/elasticsearch/bin/plugin -i elasticsearch/marvel/latest

ADD conf/elasticsearch.default /etc/default/elasticsearch
ADD conf/elasticsearch.yml /etc/elasticsearch/elasticsearch.yml