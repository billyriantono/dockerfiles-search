FROM ruby:2.6-alpine

RUN mkdir /usr/src/app
WORKDIR /usr/src/app

RUN bundle init
RUN sed -i -e 's/# gem "rails"/gem "rails"/' Gemfile

# For installing Nokogiri (ref: https://copo.jp/blog/2016/03/alpine-%E3%81%AE-ruby-%E3%81%AE%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%81%AB-nokogiri-%E3%82%92%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB/ )
RUN apk add --no-cache build-base libxml2-dev libxslt-dev

RUN bundle install

# For installing sqlite3
RUN apk add --no-cache sqlite-dev

RUN bundle exec rails new . --skip-test --skip-sprockets --force

# Without this, fails to exexute rails c / rails s.
RUN apk add --no-cache tzdata

EXPOSE 3000
CMD ["sh"]
