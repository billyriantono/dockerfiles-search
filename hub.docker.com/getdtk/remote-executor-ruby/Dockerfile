FROM ruby:2.6

RUN mkdir /app
WORKDIR /app

ADD Gemfile /app/
RUN bundle install -j 8

ADD . /app
ENTRYPOINT ["ruby", "start.rb"]
