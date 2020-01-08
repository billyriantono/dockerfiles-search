FROM ruby:2.6.4
RUN mkdir /app
WORKDIR /app
ADD . /app
RUN bundle install
CMD bundle exec puma config.ru -p $PORT -e production
