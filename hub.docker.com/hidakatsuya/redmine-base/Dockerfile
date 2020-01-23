FROM ruby:2.3-slim

MAINTAINER Katsuya HIDAKA <hidakatsuya@gmail.com>

ENV REDMINE_VERSION 3.1.7

WORKDIR /usr/src/redmine

RUN apt-get update
RUN apt-get install -y \
  wget \
  gcc \
  make \
  patch \
  libmagickcore-dev \
  libmagickwand-dev \
  libffi-dev \
  libsqlite3-dev \
  imagemagick \
  fonts-ipafont \
  libsqlite3-0

RUN wget -O redmine.tar.gz "https://www.redmine.org/releases/redmine-${REDMINE_VERSION}.tar.gz" \
      	&& tar -xvf redmine.tar.gz --strip-components=1 \
      	&& rm redmine.tar.gz files/delete.me log/delete.me

RUN touch ./config/database.yml
RUN for rails_env in development test production; do \
        echo "$rails_env:" >> ./config/database.yml; \
        echo "  adapter: sqlite3" >> ./config/database.yml; \
        echo "  database: db/$rails_env.sqlite3" >> ./config/database.yml; \
        echo "  timeout: 500" >> ./config/database.yml; \
    done
