FROM ruby:2.7.0-alpine

RUN apk update && apk upgrade --no-cache && apk add --no-cache build-base libxml2-dev libxslt-dev

WORKDIR /app
COPY Gemfile .
RUN bundle install
COPY . /app

EXPOSE 4567

CMD ["ruby", "app.rb"]
