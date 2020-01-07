FROM ubuntu:14.04
MAINTAINER Luke Closs <me@luk.ec>

RUN apt-get update
RUN apt-get install -y tar xz-utils wget libpq-dev

ENV POSTGREST_VERSION 0.3.0.3
RUN wget https://github.com/begriffs/postgrest/releases/download/v${POSTGREST_VERSION}/postgrest-${POSTGREST_VERSION}-ubuntu.tar.xz
RUN tar --xz -xvf postgrest-${POSTGREST_VERSION}-ubuntu.tar.xz
RUN mv postgrest /usr/local/bin/postgrest

ENV POSTGREST_DBNAME database
ENV POSTGREST_DBUSER user
ENV POSTGREST_DBPASS password
ENV POSTGREST_ANON   postgres

CMD postgrest postgres://${POSTGREST_DBUSER}:${POSTGREST_DBPASS}@${POSTGRES_PORT_5432_TCP_ADDR}:${POSTGRES_PORT_5432_TCP_PORT}/${POSTGREST_DBNAME} \
              --port 3000 \
              --schema public \
              --anonymous ${POSTGREST_ANON} \
              --pool 200

EXPOSE 3000

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
