# FROM scratch
# FROM debian:jessie
# FROM buildpack-deps:jessie
# FROM tensho/rbenv
FROM tensho/ruby
MAINTAINER Andrew Babichev <andrew.babichev@gmail.com>

ENV RAILS_VERSION 4.2.4

# Install nodejs
RUN apt-get update && apt-get install -y nodejs

# Install qt
RUN apt-get update && apt-get install -y qt5-default libqt5webkit5-dev

# Install db dev deps
RUN apt-get update && apt-get install -y mysql-client postgresql-client sqlite3

# Install rails
RUN gem install rails --version "$RAILS_VERSION"
