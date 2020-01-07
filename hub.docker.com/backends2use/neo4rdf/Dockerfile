FROM       kbastani/docker-neo4j:2.2.1

ENV HDFS_HOST hdfs://hdfs:9000

#*******************************************************************************

WORKDIR /var/lib/neo4j/plugins

RUN wget -c https://github.com/niclashoyer/neo4j-sparql-extension/releases/download/1.0.0/neo4j-sparql-extension-1.0.0.jar

#RUN wget -c https://github.com/thinkaurelius/neo4j-gremlin-plugin/releases/download/2.1.6/neo4j-gremlin-plugin-tp3-2.1.6-server-plugin.zip
#RUN unzip neo4j-gremlin-plugin-tp3-2.1.6-server-plugin.zip
#RUN rm -f neo4j-gremlin-plugin-tp3-2.1.6-server-plugin.zip

#*******************************************************************************

WORKDIR /var/lib/neo4j/conf

RUN sed -i "s|org.neo4j.server.thirdparty_jaxrs_classes=extension=/service|org.neo4j.server.thirdparty_jaxrs_classes=de.unikiel.inf.comsys.neo4j=/rdf|g" neo4j-server.properties

#*******************************************************************************

WORKDIR /var/lib/neo4j

EXPOSE 7474
EXPOSE 1337

# Mount a volume for persistent data
VOLUME /opt/data

# Set the bootstrap script on container run
ENV BOOTSTRAP /etc/bootstrap.sh

CMD ["/etc/bootstrap.sh", "-d"]
