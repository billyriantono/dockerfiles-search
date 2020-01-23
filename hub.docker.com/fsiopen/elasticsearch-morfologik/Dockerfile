FROM elasticsearch:5.3.0

WORKDIR /usr/share/elasticsearch
USER root
RUN bin/elasticsearch-plugin install http://central.maven.org/maven2/pl/allegro/tech/elasticsearch/plugin/elasticsearch-analysis-morfologik/5.3.0/elasticsearch-analysis-morfologik-5.3.0-plugin.zip
