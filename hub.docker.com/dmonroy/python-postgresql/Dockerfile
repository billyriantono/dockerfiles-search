FROM python:3.6.1
RUN wget -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | apt-key add - \
  && echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
  && apt-get update \
  && apt-get install postgresql-9.5 -y

ADD pg_hba.conf /etc/postgresql/9.5/main/pg_hba.conf
