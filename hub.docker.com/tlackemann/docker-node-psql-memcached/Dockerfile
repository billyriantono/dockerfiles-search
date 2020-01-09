FROM node:4.4.2-slim
MAINTAINER Thomas Lackemann <tommylackemann@gmail.com>

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' >> /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update
RUN apt-get install -y postgresql-9.4 postgresql-client-9.4
RUN apt-get install -y memcached
RUN apt-get install -y sudo
RUN service postgresql start && \
  sudo -u postgres psql -c "CREATE USER test WITH PASSWORD 'test' CREATEUSER"
