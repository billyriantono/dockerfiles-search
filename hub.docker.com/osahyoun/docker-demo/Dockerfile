FROM ruby:2.2.2

RUN mkdir /app
WORKDIR /app

ADD Gemfile* /app/

RUN bundle install --jobs 20 --retry 5

EXPOSE 3000
ADD . /app

#CMD bundle exec puma -b tcp://0.0.0.0 -p 3000 -w 4 -t 1:1

#CMD bundle exec rails s -b 0.0.0.0

