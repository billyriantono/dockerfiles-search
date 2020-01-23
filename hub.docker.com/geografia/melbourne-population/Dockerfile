FROM ruby:2.3.1-slim

ENV RAILS_ROOT=/usr/app/melbournepopulation
ENV RAILS_ENV=production
ENV RACK_ENV=production
ENV PGPASSWORD=1fHlwzq3MDE=
ENV POSTGRES_PASSWORD=1fHlwzq3MDE=
ENV SECRET_KEY_BASE=9b3c124892648246da5f20ffa88a45073c61f7f1cf371aa274649ab7cbca357c076fad5a55bbd4995c3fad74b9a3a21aa50beff7a3f9825c328befa095f8d7b5
ENV RAILS_LOG_TO_STDOUT=true

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev postgresql-client libproj-dev nodejs

RUN mkdir -p $RAILS_ROOT/tmp/pids
WORKDIR $RAILS_ROOT

COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock

RUN gem install rake bundler
RUN bundle check || bundle install --without development test -j4

COPY config/puma.rb config/puma.rb

COPY . .

RUN mkdir -p /etc/nginx/conf.d/
COPY ./containers/production/nginx.conf /etc/nginx/conf.d/default.conf

RUN DB_ADAPTER=nulldb bundle exec rake assets:precompile RAILS_ENV=production

EXPOSE 3000
