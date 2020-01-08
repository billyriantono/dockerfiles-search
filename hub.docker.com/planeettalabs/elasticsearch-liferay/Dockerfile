FROM docker.elastic.co/elasticsearch/elasticsearch:6.5.4

# https://dev.liferay.com/fr/discover/deployment/-/knowledge_base/7-0/upgrading-to-elasticsearch-6
RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu && \
  /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-kuromoji && \
  /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-smartcn && \
  /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-stempel
