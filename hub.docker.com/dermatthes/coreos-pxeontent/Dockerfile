# Inspired by Martin Frys https://github.com/martineez/pagila
# Use Debian (stretch-slime) instead of for Alpine base

FROM postgres:10
MAINTAINER Derek Williams <derek61@gmail.com>

ENV POSTGRES_DB pagila
#ENV POSTGRES_USER pagila
#ENV POSTGRES_PASSWORD pagila

#ENV POSTGRES_DB pagila
ENV POSTGRES_USER pagila
ENV POSTGRES_PASSWORD pagila

COPY *.sh /docker-entrypoint-initdb.d/
COPY *.sql /docker-entrypoint-initdb.d/dump/

EXPOSE 5432
CMD ["postgres"]