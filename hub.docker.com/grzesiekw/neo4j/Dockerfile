FROM dockerfile/java:oracle-java8
MAINTAINER gw <g.wilkowicz@gmail.com>

RUN apt-get update && apt-get install -y lsof && apt-get clean && \
    mkdir -p /var/lib/neo4j
RUN curl http://neo4j.com/artifact.php?name=neo4j-community-2.1.6-unix.tar.gz -o /tmp/neo4j-2.1.6.tar.gz && \
    tar -xvzf /tmp/neo4j-2.1.6.tar.gz -C /var/lib/neo4j && rm /tmp/neo4j-2.1.6.tar.gz

RUN sed -i 's/#org.neo4j.server.webserver.address/org.neo4j.server.webserver.address/g' /var/lib/neo4j/neo4j-community-2.1.6/conf/neo4j-server.properties

EXPOSE 7474 1337

CMD ["/var/lib/neo4j/neo4j-community-2.1.6/bin/neo4j", "console"]
