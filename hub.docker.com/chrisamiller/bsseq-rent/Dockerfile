FROM neo4j:3.5
RUN mkdir /plugins
WORKDIR /plugins
RUN apk add --no-cache --quiet wget
RUN wget https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/3.5.0.2/apoc-3.5.0.2-all.jar
ENV NEO4J_apoc_export_file_enabled true
ENV NEO4J_apoc_import_file_enabled true
ENV NEO4J_apoc_import_file_use__neo4j__config true
ENV NEO4J_dbms_security_procedures_unrestricted algo.\\\*,apoc.\\\*
