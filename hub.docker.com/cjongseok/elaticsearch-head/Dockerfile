#FROM cjongseok/oracle-jdk:1.8.0_77
FROM elasticsearch:2.3.3

RUN set -u \
        && /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head

VOLUME /usr/share/elasticsearch/data        

EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
