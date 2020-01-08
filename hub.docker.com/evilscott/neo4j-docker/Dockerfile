FROM neo4j:3.5.8
ENV APOC_VERSION 3.5.0.4
ENV ALGOS_VERSION 3.5.8.0
ENV POSTGRES_JDBC_VERSION 42.2.6
ENV APOC_URL https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/$APOC_VERSION/apoc-$APOC_VERSION-all.jar
ENV ALGOS_URL http://s3-eu-west-1.amazonaws.com/com.neo4j.graphalgorithms.dist/neo4j-graph-algorithms-$ALGOS_VERSION-standalone.jar
ENV POSTGRES_JDBC_URL https://jdbc.postgresql.org/download/postgresql-$POSTGRES_JDBC_VERSION.jar
RUN (cd /var/lib/neo4j/plugins && curl -OL $APOC_URL)
RUN (cd /var/lib/neo4j/plugins && curl -OL $ALGOS_URL)
RUN (cd /var/lib/neo4j/plugins && curl -OL $POSTGRES_JDBC_URL)
EXPOSE 7474 7687
