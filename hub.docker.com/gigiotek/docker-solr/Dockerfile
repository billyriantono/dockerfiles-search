FROM solr
WORKDIR /opt/solr/server/solr/
ADD core/solr1_gettingstarted /opt/solr/server/solr/gettingstarted
USER root
RUN chown -R solr /opt/solr/server/solr
USER solr