FROM docker.elastic.co/elasticsearch/elasticsearch:7.4.2

COPY custom-entrypoint.sh /custom-entrypoint.sh

ENTRYPOINT ["/custom-entrypoint.sh"]
CMD ["elasticsearch"]
