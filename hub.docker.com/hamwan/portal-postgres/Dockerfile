FROM postgres
ADD ./0-functions.sql /docker-entrypoint-initdb.d/
ADD ./1-powerdns-create-user-db.sh /docker-entrypoint-initdb.d/
ADD ./2-powerdns-create-tables.sql /docker-entrypoint-initdb.d/
