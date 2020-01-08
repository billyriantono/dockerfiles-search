FROM solr:7.6-alpine

ENV SEARCH_API_SOLR_VER="7.x-1.14"
ENV SOLR_CONF_VER="7.x"

# Install curl
USER root
RUN apk add --no-cache curl
RUN rm -rf /opt/solr/server/solr/configsets/_default/conf
USER solr

# Add drupal specific solr config
COPY --chown=solr:solr conf /opt/solr/server/solr/configsets/_default/conf

HEALTHCHECK --start-period=60s --interval=120s --retries=3 CMD [ "curl","-fq","http://localhost:8983/solr/admin/cores?action=STATUS" ]
