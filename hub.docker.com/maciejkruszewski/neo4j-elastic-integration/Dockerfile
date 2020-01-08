FROM neo4j:latest
ADD graphware.conf /var/lib/neo4j
ADD graphaware-server-community-all-3.3.2.52.jar /var/lib/neo4j/plugins
ADD graphaware-neo4j-to-elasticsearch-3.3.2.52.7.jar /var/lib/neo4j/plugins
RUN cat /var/lib/neo4j/graphware.conf >> /var/lib/neo4j/conf/neo4j.conf