FROM jhonathas/ruby:2.1.2

MAINTAINER Jhonathas Matos <jhonathas@gmail.com>

RUN apt-get update

# Dependence of Identiticache gem
RUN apt-get install -y memcached

# Dependence of pg gem
RUN apt-get install -y postgresql-contrib-9.3
RUN apt-get install -y nodejs --no-install-recommends

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

ONBUILD RUN gem update --system
ONBUILD RUN gem install bundler

ONBUILD COPY Gemfile .

ONBUILD RUN bundle install