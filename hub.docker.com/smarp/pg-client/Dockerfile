FROM debian:jessie
MAINTAINER TruongSinh Tran-Nguyen <truongsinh@smarp.com>

# https://docs.docker.com/engine/examples/postgresql_service/
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list

RUN apt-get update
RUN apt-get install postgresql-client-9.6 git -y
RUN apt-get upgrade bash -y

ENV PGHOST=postgres
ENV PGUSER=postgres
ENV PGSSLMODE=disable

CMD ["/usr/bin/psql"]
