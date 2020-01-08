FROM blacktop/elasticsearch:1.7

# Install elasticsearch Plugins
RUN plugin install lmenezes/elasticsearch-kopf/v1.6.2
RUN plugin install mobz/elasticsearch-head

# Add path.repo to settings
RUN echo "path.repo: \${ES_PATH_REPO}" >> /usr/share/elasticsearch/config/elasticsearch.yml
RUN echo "cluster.name: \${ES_CLUSTER_NAME}" >> /usr/share/elasticsearch/config/elasticsearch.yml
RUN echo "script.inline: on" >> /usr/share/elasticsearch/config/elasticsearch.yml