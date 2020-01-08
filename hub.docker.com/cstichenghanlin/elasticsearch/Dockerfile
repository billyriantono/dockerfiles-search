FROM docker.elastic.co/elasticsearch/elasticsearch:6.3.1
MAINTAINER icrdc-yichengchiu
RUN echo '# allow origin' >> /usr/share/elasticsearch/config/elasticsearch.yml
RUN echo 'http.cors.enabled: true' >> /usr/share/elasticsearch/config/elasticsearch.yml
RUN echo 'http.cors.allow-origin: "*"' >> /usr/share/elasticsearch/config/elasticsearch.yml
