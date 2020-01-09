FROM ruby:2.6.2-alpine

RUN gem install bundler --no-doc && bundle config --global frozen 1

WORKDIR /app

COPY . /app/

RUN bundle install -j 3

RUN rake

ENTRYPOINT ["/app/bin/ecsbatch", "start"]
