FROM ruby:2.5-alpine

# see http://guides.rubyonrails.org/command_line.html#rails-dbconsole
RUN apk add --no-cache nodejs mysql-client postgresql-client sqlite build-base sqlite-dev tzdata

ENV RAILS_VERSION 5.2.2
RUN gem install rails --version "$RAILS_VERSION"

RUN mkdir -p /app
WORKDIR /app

COPY Gemfile .
RUN bundle install && rm Gemfile

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
