FROM neo4j:3.5
RUN echo "dbms.security.procedures.unrestricted=apoc.trigger.*,apoc.meta.*" >> /var/lib/neo4j/conf/neo4j.conf
RUN mkdir /plugins/
ADD --chown=neo4j:neo4j https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/3.5.0.4/apoc-3.5.0.4-all.jar /plugins/
#ADD https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/3.4.0.7/apoc-3.4.0.7-all.jar /plugins/apoc.jar
#dbms.security.procedures.unrestricted=apoc.*

