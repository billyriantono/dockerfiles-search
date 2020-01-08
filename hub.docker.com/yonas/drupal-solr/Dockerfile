FROM solr:5.5-alpine
MAINTAINER Yonas Yanfa <yonas@savaslabs.com>

COPY solr /opt/solr/server/solr/mycores

USER root
RUN chown -R solr:solr /opt/solr/server/solr/mycores
USER solr

VOLUME /opt/solr/server/solr/mycores/solr
EXPOSE 8983

WORKDIR /opt/solr

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["solr-foreground"]
