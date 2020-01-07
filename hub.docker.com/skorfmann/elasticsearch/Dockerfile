# Elasticsearch
# docker pull skorfmann/elasticsearch
FROM barnybug/elasticsearch
MAINTAINER Sebastian Korfmann <korfmann.sebastian@gmail.com>

RUN /elasticsearch/bin/plugin -install elasticsearch/elasticsearch-river-twitter/2.4.1

ADD elasticsearch.yml /elasticsearch/config/elasticsearch.yml

VOLUME ["/data", "/logs"]

EXPOSE 9200 9300
CMD ["elasticsearch/bin/elasticsearch"]
