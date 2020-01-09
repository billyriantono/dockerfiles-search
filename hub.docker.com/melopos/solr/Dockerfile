FROM guywithnose/solr:4.10.2
# You can change the FROM Instruction to your existing images if you like and build it with same tag
MAINTAINER melopos - support@melopos.com

RUN rm -Rf /opt/solr/example/solr/collection1/

COPY collection1/ /opt/solr/example/solr/production/

USER root

RUN chown solr:solr -R /opt/solr/example/solr/production/

USER solr
