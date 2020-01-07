FROM postgres:10.1-alpine

LABEL maintainer="andre.burgaud@gmail.com"

ADD sql/*.sql /docker-entrypoint-initdb.d/
