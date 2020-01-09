FROM ruby:2.5.0

RUN apt-get update -qq
RUN apt-get install -y build-essential
RUN apt-get install -y libpq-dev
RUN apt-get install -y nodejs

ENV PROJECT_ROOT /usr/src/app
ENV GEM_HOME $PROJECT_ROOT/vendor/bundle
ENV BUNDLE_PATH $PROJECT_ROOT/vendor/bundle
ENV BUNDLE_JOBS 2

RUN mkdir -p $PROJECT_ROOT

WORKDIR $PROJECT_ROOT

COPY Gemfile .
COPY Gemfile.lock .

RUN bundle install

COPY . .
