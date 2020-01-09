FROM ruby:2.3.0

RUN apt-get update -qq && apt-get -y install \
  nodejs \
  imagemagick

WORKDIR /app

ENV PATH=$PATH:/app/vendor/bundle/ruby/2.3.0/bin
ENV GEM_PATH=/usr/local/bundle:/root/.gem/ruby/2.3.0:/usr/local/lib/ruby/gems/2.3.0:/app/vendor/bundle/ruby/2.3.0:/app/vendor/bundle/ruby/2.3.0
