FROM ruby:2.5
LABEL Name=konomi_be_srvc Version=0.0.3
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs
RUN mkdir /app
WORKDIR /app
COPY Gem* /app/
RUN bundle install
COPY . /app/

EXPOSE 8001

ENTRYPOINT sleep infinity