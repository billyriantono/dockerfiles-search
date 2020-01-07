FROM traxair/oracle-java7:latest

ENV DEBIAN_FRONTEND noninteractive
ENV ES_VERSION 1.5

RUN wget -O - http://packages.elasticsearch.org/GPG-KEY-elasticsearch | apt-key add - && \
    echo "deb http://packages.elasticsearch.org/elasticsearch/$ES_VERSION/debian stable main" | tee -a /etc/apt/sources.list.d/elasticsearch.list && \
    apt-get update && \
    apt-get install -y elasticsearch && \
    mkdir -p /usr/share/elasticsearch/config && \
    ln -s /etc/elasticsearch/elasticsearch.yml /usr/share/elasticsearch/config/elasticsearch.yml && \
    ln -s /etc/elasticsearch/logging.yml /usr/share/elasticsearch/config/logging.yml && \
    apt-get clean && \
    apt-get purge

VOLUME ["/var/lib/elasticsearch", "/usr/share/elasticsearch/data", "/usr/share/elasticsearch/logs"]

EXPOSE 9200 9300

ONBUILD ENTRYPOINT ["/usr/share/elasticsearch/bin/elasticsearch"]
