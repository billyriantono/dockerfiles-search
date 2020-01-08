FROM postgres:alpine

ENV POSTGRES_USER hiveuser
ENV POSTGRES_PASSWORD hivepassword
ADD files /docker-entrypoint-initdb.d/
