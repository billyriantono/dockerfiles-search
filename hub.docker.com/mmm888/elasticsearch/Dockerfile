FROM elasticsearch:5.6-alpine

ENV ES_JAVA_OPTS "-Xms256m -Xmx256m"

RUN : "Add symbolic link for volumes" && \
    ln -s /usr/share/elasticsearch/data / && \
    : "Install Japanese search for growi" && \
    ./bin/elasticsearch-plugin list | grep -q analysis-kuromoji || ./bin/elasticsearch-plugin install analysis-kuromoji && \
    ./bin/elasticsearch-plugin list | grep -q analysis-icu || ./bin/elasticsearch-plugin install analysis-icu

ENTRYPOINT ["/docker-entrypoint.sh", "elasticsearch"]
