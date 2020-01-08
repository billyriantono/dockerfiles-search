FROM java:openjdk-7

MAINTAINER John Allen, john.allen@connexiolabs.com

ENV NEO4J_VERSION 2.3.0-M01

RUN mkdir -p /tmp/downloads && \
    cd /tmp/downloads && \
    curl http://dist.neo4j.org/neo4j-community-2.3.0-M01-unix.tar.gz | tar xz && \
    mv neo4j-community-2.3.0-M01 /var/lib/neo4j && \
    sed -i "s|#node_auto_indexing|node_auto_indexing|g" /var/lib/neo4j/conf/neo4j.properties && \
    sed -i "s|#node_keys_indexable|node_keys_indexable|g" /var/lib/neo4j/conf/neo4j.properties && \
    echo "remote_shell_host=0.0.0.0" >> /var/lib/neo4j/conf/neo4j.properties

EXPOSE 7474
EXPOSE 1337

WORKDIR /

COPY launch.sh /

CMD ["/launch.sh"]
