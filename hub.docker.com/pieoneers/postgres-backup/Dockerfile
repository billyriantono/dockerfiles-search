FROM ruby:2.3.0

RUN apt-get update -qq && apt-get install -y \
  postgresql-client-9.4 \
  cron \
  rsyslog

ENV APP_PATH /app/user/

RUN mkdir -p $APP_PATH
WORKDIR $APP_PATH

ADD Gemfile* ./
RUN bundle install

ADD . ./

ADD docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
