FROM makuk66/docker-solr:latest

MAINTAINER kfm@docstream.no

# NB docker 1.0.1 has no wildcard support :)
COPY stopwords_no.txt /opt/ds/


RUN /opt/solr/bin/solr start && \
  /opt/solr/bin/solr create -c c1 -d basic_configs -p 8983 && \
  /opt/solr/bin/solr stop && \
  cp /opt/ds/stopwords* /opt/solr/server/solr/c1/conf/stopwords.txt

# howto backup
# docker cp CONTAINERID:/opt/solr/server/solr/c1/data /var/backupdir/solr/c1
