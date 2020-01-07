FROM ruby:2.3.3

ENV PG_MAJOR 9.6

RUN apt-get update \
  && apt-get install -y wget ca-certificates sudo

RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main' > /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

RUN apt-get update -yqqq \
  && apt-get install -y postgresql-common \
  && apt-get install -y postgresql-$PG_MAJOR postgresql-contrib-$PG_MAJOR \
  && apt-get -qq -y --force-yes install apt-utils bzip2 nodejs-legacy npm \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm install -g phantomjs-prebuilt

RUN wget -qO- https://toolbelt.heroku.com/install.sh | sh

RUN /etc/init.d/postgresql start \
  && sudo -u postgres sh -c 'createuser ci_test & createdb ci_test' \
  && sudo -u postgres psql -c "ALTER USER ci_test PASSWORD 'ci_test' CREATEDB SUPERUSER;"
