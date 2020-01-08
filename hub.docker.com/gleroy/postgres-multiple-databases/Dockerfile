FROM postgres:latest

COPY ./create-users.sh /docker-entrypoint-initdb.d/10_create-user.sh
COPY ./create-databases.sh /docker-entrypoint-initdb.d/20_create-databases.sh