FROM debian:buster-slim

COPY ./key.asc /tmp/key.asc

RUN apt-get -qq update && \
    apt-get -qq install ssh gnupg 1> /dev/null && \
    apt-key add /tmp/key.asc && \
    printf "\ndeb http://apt.postgresql.org/pub/repos/apt/ buster-pgdg main\n" >> "/etc/apt/sources.list.d/pgdg.list" && \
    apt-get -qq update && \
    apt-get -qq install postgresql-11 postgresql-11-repmgr 1> /dev/null && \
    apt-get -qq upgrade 1> /dev/null
