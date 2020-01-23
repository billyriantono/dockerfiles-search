FROM mysql:5.6

ADD setup/1-SCHEMA.sql /docker-entrypoint-initdb.d/1-SCHEMA.sql
ADD setup/2-PRIVILEGES.sql /docker-entrypoint-initdb.d/2-PRIVILEGES.sql 
ADD setup/3-ENTRIES.sql /docker-entrypoint-initdb.d/3-ENTRIES.sql
