FROM python:3.5
MAINTAINER Davur Clementsen <davur@davur.net>
RUN apt-get update \
  && apt-get install -y postgresql postgresql-contrib \
  && apt-get install sudo \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN /etc/init.d/postgresql start \
  && sudo -u postgres sh -c 'createuser root & createdb docker'
