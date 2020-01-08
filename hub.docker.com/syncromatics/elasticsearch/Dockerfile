FROM elasticsearch:2.4.2
HEALTHCHECK --interval=1s --timeout=5s --start-period=1s --retries=60 \
    CMD curl http://localhost:9200/ || exit 1

RUN /usr/share/elasticsearch/bin/plugin install --batch delete-by-query