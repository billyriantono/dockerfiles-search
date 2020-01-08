FROM docker.elastic.co/elasticsearch/elasticsearch:6.2.1

RUN bin/elasticsearch-plugin install repository-azure

RUN bin/elasticsearch-plugin install https://distfiles.compuscene.net/elasticsearch/elasticsearch-prometheus-exporter-6.2.1.0.zip

