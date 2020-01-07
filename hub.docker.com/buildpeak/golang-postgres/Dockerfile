FROM golang

RUN apt-get update \
    && apt-get install -y postgresql \
    && apt-get clean

ENV PG_MAJOR 11
ENV PATH $PATH:/usr/lib/postgresql/$PG_MAJOR/bin
ENV PGDATA /var/lib/postgresql/data

RUN sed -i 's/peer$/trust/g' /etc/postgresql/$PG_MAJOR/main/pg_hba.conf
