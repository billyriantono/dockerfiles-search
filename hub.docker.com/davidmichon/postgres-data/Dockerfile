FROM busybox

COPY postgres-setup /docker-entrypoint-initdb.d

VOLUME ["/docker-entrypoint-initdb.d", "/var/lib/postgresql/data", "/var/log/postgresql"]
