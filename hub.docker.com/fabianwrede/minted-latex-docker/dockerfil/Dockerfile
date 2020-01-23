FROM ruby:2.6.5

ENV APP_ROOT /app
RUN mkdir $APP_ROOT
WORKDIR $APP_ROOT
ADD ./Gemfile $APP_ROOT/Gemfile
ADD ./Gemfile.lock $APP_ROOT/Gemfile.lock
RUN bundle install
ADD . $APP_HOME
