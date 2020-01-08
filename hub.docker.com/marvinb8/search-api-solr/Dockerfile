FROM makuk66/docker-solr:5
USER root
COPY ./myindex /opt/solr/server/solr/myindex
RUN chown -R solr:solr /opt/solr/server/solr/myindex
USER solr
CMD ["/bin/bash","-c" ,"/opt/solr/bin/solr -m 1g -f"]
