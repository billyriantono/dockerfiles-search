FROM docker.elastic.co/elasticsearch/elasticsearch:5.6.1
USER elasticsearch
RUN elasticsearch-plugin install -v -b https://github.com/vvanholl/elasticsearch-prometheus-exporter/releases/download/5.6.1.0/elasticsearch-prometheus-exporter-5.6.1.0.zip
RUN elasticsearch-plugin remove x-pack
USER elasticsearch
