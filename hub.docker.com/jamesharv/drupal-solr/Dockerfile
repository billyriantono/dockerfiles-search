FROM ubuntu:14.04

MAINTAINER James Harvey "james@webmarkdesigns.com.au"

ENV SOLR_VERSION 4.4.0
ENV SOLR solr-$SOLR_VERSION
ENV SOLR_USER solr
ENV DRUPAL_APACHESOLR_VERSION 7.x-1.7
ENV DRUPAL_SEARCH_API_VERSION 7.x-1.8

VOLUME /mnt

RUN apt-get -y update
RUN apt-get -y install openjdk-7-jdk
RUN groupadd -r $SOLR_USER
RUN apt-get -y install wget
RUN wget http://archive.apache.org/dist/lucene/solr/$SOLR_VERSION/$SOLR.tgz
RUN tar -xvf $SOLR.tgz
RUN mv $SOLR /opt/solr
RUN useradd -r -g $SOLR_USER $SOLR_USER
RUN mv /opt/solr/example/multicore/core0 /opt/solr/example/multicore/apachesolr
RUN mv /opt/solr/example/multicore/core1 /opt/solr/example/multicore/search_api
RUN sed -i 's@<core name="core0" instanceDir="core0" />@<!-- core -->@g' /opt/solr/example/multicore/solr.xml
RUN sed -i 's@<core name="core1" instanceDir="core1" />@@g' /opt/solr/example/multicore/solr.xml
RUN cd /tmp
RUN wget http://ftp.drupal.org/files/projects/apachesolr-$DRUPAL_APACHESOLR_VERSION.tar.gz && tar -xvzf apachesolr-$DRUPAL_APACHESOLR_VERSION.tar.gz
RUN wget http://ftp.drupal.org/files/projects/search_api_solr-$DRUPAL_SEARCH_API_VERSION.tar.gz && tar -xvzf search_api_solr-$DRUPAL_SEARCH_API_VERSION.tar.gz
RUN rm -rf /opt/solr/example/multicore/apachesolr/conf
RUN cp -r apachesolr/solr-conf/solr-4.x /opt/solr/example/multicore/apachesolr/conf
RUN rm -rf /opt/solr/example/multicore/search_api/conf
RUN cp -r search_api_solr/solr-conf/4.x /opt/solr/example/multicore/search_api/conf
RUN chown -R $SOLR_USER:$SOLR_USER /opt/solr/example

EXPOSE 8983
EXPOSE 8984

ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

WORKDIR /opt/solr/example

ENTRYPOINT /entrypoint.sh
CMD ["-Dsolr.solr.home=/mnt/solr"]
