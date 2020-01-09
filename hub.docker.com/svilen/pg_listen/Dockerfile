FROM postgres:9.6
LABEL maintainer Svilen Sabev <svilensabev@gmail.com>

RUN apt-get update && \
    apt-get install -y libpq-dev git make pkg-config clang

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git clone https://github.com/begriffs/pg_listen.git
WORKDIR /pg_listen
RUN make

ARG POSTGRES_DB_URI
ENV POSTGRES_DB_URI="$POSTGRES_DB_URI"

CMD ./pg_listen ${POSTGRES_DB_URI} ddl_command_end "kill -HUP `pgrep postgrest`"
