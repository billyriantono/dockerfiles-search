FROM frodenas/java7
MAINTAINER Woorank <dev@woorank.com>

ENV ES_PKG_NAME elasticsearch-1.4.4
ENV ES_HEAP_SIZE 1g
ENV MAX_LOCKED_MEMORY unlimited
ENV MAX_MAP_COUNT 262144

# Install Elasticsearch 1.4.4
RUN cd /tmp && \
    wget https://download.elasticsearch.org/elasticsearch/elasticsearch/$ES_PKG_NAME.tar.gz && \
    tar xvzf $ES_PKG_NAME.tar.gz && \
    mv /tmp/$ES_PKG_NAME /opt/elasticsearch && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ADD elasticsearch.yml /opt/elasticsearch/config/elasticsearch.yml

CMD ["/opt/elasticsearch/bin/elasticsearch"]

# Expose listen port
EXPOSE 9200
EXPOSE 9300

# Expose our data and logs volumes
VOLUME ["/data", "/logs", "/work"]
