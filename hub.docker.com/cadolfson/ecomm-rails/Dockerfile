FROM ruby:2.5.1

ENV RAILS_ENV='production'
ENV RACK_ENV='production'
ENV SECRET_KEY_BASE='123456789'

RUN mkdir /code
WORKDIR /code

RUN apt-get update && apt-get install -y \
      build-essential \
      libpq-dev \
      nodejs \
      imagemagick \
    && rm -rf /var/lib/apt/lists/*

COPY Gemfile /code/Gemfile
COPY Gemfile.lock /code/Gemfile.lock

RUN bundle install --jobs 20 --retry 5 --without development test

COPY . /code

RUN bundle exec rake assets:precompile