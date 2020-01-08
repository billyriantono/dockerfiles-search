FROM ruby:2.2
MAINTAINER Ryan Guo<ryan@islandzero.net>

# install Node.js, PostgreSQL and Sqlite3
RUN apt-get update && apt-get install -y nodejs postgresql-client sqlite3 --no-install-recommends && rm -rf /var/lib/apt/lists/*

