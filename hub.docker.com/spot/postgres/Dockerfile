FROM mdillon/postgis:latest
ADD fix-acl.sh /docker-entrypoint-initdb.d/
RUN /docker-entrypoint-initdb.d/fix-acl.sh
