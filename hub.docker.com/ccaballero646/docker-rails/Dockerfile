FROM ruby:slim
RUN apt-get update -qq &&  \
    apt-get upgrade -y && \
    apt-get install -y build-essential libpq-dev sqlite3 nodejs
RUN mkdir /app
WORKDIR /app
COPY Gemfile /app
COPY Gemfile.lock /app
RUN bundle install