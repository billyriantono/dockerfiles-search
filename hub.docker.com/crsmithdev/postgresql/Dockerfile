FROM crsmithdev/ubuntu:14.04

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main 9.4" > /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN DEBIAN_FRONTEND=noninteractive apt-get -q update && apt-get install -yq \
    postgresql-9.4 \
    postgresql-contrib-9.4 \
    postgresql-client-9.4

RUN mkdir -p /data
RUN chown postgres:postgres /data

ADD postgresql.conf /etc/postgresql/9.4/main/postgresql.conf
ADD pg_hba.conf /etc/postgresql/9.4/main/pg_hba.conf
ADD start /start

VOLUME ["/data"]
EXPOSE 5432

CMD ["./start"]

