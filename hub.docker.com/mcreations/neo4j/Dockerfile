## -*- docker-image-name: "mcreations/neo4j" -*-

FROM neo4j:3.4.4

LABEL maintainer="Kambiz Darabi <darabi@m-creations.net>"
LABEL vendor="mcreations"

ENV PASSWORD "neo4j"
ENV NEO4J_dbms_security_procedures_unrestricted "apoc.\*"
ENV NEO4J_apoc_trigger_enabled "true"

ADD image/root /

ENTRYPOINT ["/start-neo"]

