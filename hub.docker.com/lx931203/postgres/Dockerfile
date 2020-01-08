FROM lx931203/base
LABEL maintainer "Lex Ushakov <lx.931203@gmail.com>"
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ buster-pgdg main" >> /etc/apt/sources.list
RUN wget \
  --quiet \
  -O - \
https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt update
RUN apt install \
  -y \
  --no-install-recommends \
postgresql-11 postgresql-client-11 libpq-dev postgresql-server-dev-10 pgadmin4
COPY ./pg_hba.conf /etc/postgresql/11/main/pg_hba.conf
ENTRYPOINT pg_ctlcluster 11 main start --foreground
