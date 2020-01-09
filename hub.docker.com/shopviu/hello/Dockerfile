FROM ruby:2.4.1-slim
RUN apt-get update -qq && apt install -y build-essential vim

ENV APP_ROOT /var/www/helloworld
RUN mkdir -p $APP_ROOT
WORKDIR $APP_ROOT
ADD Gemfile* $APP_ROOT/
RUN bundle install
ADD . $APP_ROOT

EXPOSE 7070
VOLUME $APP_ROOT

CMD ["bundle", "exec", "thin", "start", "-p", "7070"]

