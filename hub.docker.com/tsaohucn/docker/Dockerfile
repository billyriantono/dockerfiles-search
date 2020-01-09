FROM ruby:2.3

MAINTAINER Tomato <tsaohucn@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

ENV LANG C.UTF-8

# install rails && bundler
RUN /bin/bash -l -c "gem install rails --version '5.0.1' --no-ri --no-rdoc"

WORKDIR /huginn

# copy huginn config file
ADD ["src/Gemfile", "src/Gemfile.lock", "src/.env", "src/Procfile", "/huginn/"]
ADD src/lib/gemfile_helper.rb /huginn/lib/
ADD src/vendor/gems /huginn/vendor/gems

# run bundle install
RUN /bin/bash -l -c "bundle install"

# copy huginn
COPY src/. /huginn