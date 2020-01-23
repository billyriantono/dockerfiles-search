FROM java:8-jre
MAINTAINER Arun Manivannan <arun@arunma.com>

ENV ELASTICSEARCH_VERSION 1.6.0

# Install ElasticSearch
RUN wget https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-$ELASTICSEARCH_VERSION.tar.gz
RUN tar xzf elasticsearch-$ELASTICSEARCH_VERSION.tar.gz
RUN mv elasticsearch-$ELASTICSEARCH_VERSION /opt/elasticsearch
RUN rm elasticsearch-$ELASTICSEARCH_VERSION.tar.gz

#Sets cluster name and data and log configs
RUN echo -e 'cluster.name : ns-es-cluster\npath:\n data: /data\n logs: /logs' >> /opt/elasticsearch/config/elasticsearch.yml
RUN sed -i 's/es\.logger\.level\: INFO/es\.logger\.level\: DEBUG/' /opt/elasticsearch/config/logging.yml

# Install Kibana
RUN /opt/elasticsearch/bin/plugin -url https://download.elasticsearch.org/kibana/kibana/kibana-3.1.2.zip -install elasticsearch/kibana3

#VOLUME ["/data", "/logs"]

EXPOSE 9200 9300 5601

CMD ["/opt/elasticsearch/bin/elasticsearch"]
