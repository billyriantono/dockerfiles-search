FROM solr:6.6.6
USER root

COPY *.xml ./

# test env
RUN mkdir -p server/solr/test/conf
RUN cp schema.xml server/solr/test/conf/
RUN cp solrconfig.xml server/solr/test/conf/

# dev env
RUN mkdir -p server/solr/development/conf
RUN cp schema.xml server/solr/development/conf/
RUN cp solrconfig.xml server/solr/development/conf/
RUN printf "name=development\nconfig=solrconfig.xml\nschema=schema.xml\ndataDir=data" > server/solr/development/conf/core.properties

# staging env
RUN mkdir -p server/solr/staging/conf
RUN cp schema.xml server/solr/staging/conf/
RUN cp solrconfig.xml server/solr/staging/conf/
RUN printf "name=staging\nconfig=solrconfig.xml\nschema=schema.xml\ndataDir=data" > server/solr/staging/conf/core.properties

# production env
RUN mkdir -p server/solr/production/conf
RUN cp schema.xml server/solr/production/conf/
RUN cp solrconfig.xml server/solr/production/conf/
RUN printf "name=production\nconfig=solrconfig.xml\nschema=schema.xml\ndataDir=data" > server/solr/production/conf/core.properties

RUN chown -R solr server/solr

USER solr
