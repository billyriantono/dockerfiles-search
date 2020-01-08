FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.3.2

MAINTAINER Björn Heneka <heneka@jacob.de>

RUN bin/elasticsearch-plugin install -b "com.floragunn:search-guard-6:6.3.2-22.3" && \
    chmod +x /usr/share/elasticsearch/plugins/search-guard-6/tools/sgadmin.sh && \
    chmod +x /usr/share/elasticsearch/plugins/search-guard-6/tools/hash.sh
