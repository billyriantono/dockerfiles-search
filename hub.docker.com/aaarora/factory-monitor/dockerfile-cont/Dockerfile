FROM elixir:1.6.0-slim AS common

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv ACCC4CF8 && \
    echo "deb http://deb.debian.org/debian jessie-backports main contrib non-free" > /etc/apt/sources.list.d/backports.list && \
    echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' > /etc/apt/sources.list.d/postgres.list && \
    apt update -qq && \
    apt-get upgrade -y && \
    apt-get install -y psmisc gosu postgresql-client-9.6 curl build-essential git

