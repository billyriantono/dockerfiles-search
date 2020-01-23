FROM postgres:9.4

ENV SILF_USER=silf \
    SILF_DB=silf \
    SILF_PASS=changemeplease

COPY init/initdb.sql /docker-entrypoint-initdb.d/
