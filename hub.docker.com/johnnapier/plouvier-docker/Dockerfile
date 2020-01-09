FROM ruby:2.3.1
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs
RUN mkdir /myapp
WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install
# Provide dummy data to Rails so it can pre-compile assets.
RUN RAILS_ENV=production bundle exec rails assets:precompile

COPY . /myapp

CMD bundle exec unicorn -c ./config/unicorn.rb