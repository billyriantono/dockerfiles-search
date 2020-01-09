FROM chriswk/java8minimal

ENV SOLR_MAJOR_VERSION 5
ENV SOLR_MINOR_VERSION 3
ENV SOLR_PATCH_VERSION 1

RUN curl -s http://apache.uib.no/lucene/solr/5.3.1/solr-${SOLR_MAJOR_VERSION}.${SOLR_MINOR_VERSION}.${SOLR_PATCH_VERSION}.tgz\
  | tar -xzf - -C /opt \
  && rm -rf /opt/apache-solr-${SOLR_MAJOR_VERSION}.${SOLR_MINOR_VERSION}.${SOLR_PATCH_VERSION}/docs

RUN ln -s /opt/apache-solr-${SOLR_MAJOR_VERSION}.${SOLR_MINOR_VERSION}.${SOLR_PATCH_VERSION} /opt/solr${SOLR_MAJOR_VERSION}

ENV SOLR_HOME /opt/solr${SOLR_MAJOR_VERSION}
