FROM docker.elastic.co/elasticsearch/elasticsearch:5.3.0

MAINTAINER Jiri Bires <jiri.bires@ysoft.com>

#Remove X-Pack
RUN mv /usr/share/elasticsearch/plugins/x-pack /usr/share/elasticsearch/plugins/.removing-x-pack && \
    mv /usr/share/elasticsearch/plugins/.removing-x-pack /usr/share/elasticsearch/plugins/x-pack && \
    /usr/share/elasticsearch/bin/elasticsearch-plugin remove x-pack && \
    /usr/share/elasticsearch/bin/elasticsearch-plugin install --batch analysis-icu && \
    /usr/share/elasticsearch/bin/elasticsearch-plugin install --batch analysis-phonetic

