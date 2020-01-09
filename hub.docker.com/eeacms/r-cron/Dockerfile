FROM alpine

MAINTAINER michimau <mauro.michielon@eea.europa.eu>


RUN apk update
RUN apk fetch java-postgresql-jdbc curl openjdk8
RUN apk add java-postgresql-jdbc curl openjdk8 make

COPY        entrypoint.sh /
ENTRYPOINT  ["/entrypoint.sh"]
