FROM ruby:2.3.0

MAINTAINER nguyen.ha.phan@framgia.com

RUN apt update

RUN apt install -y build-essential nodejs

RUN mkdir -p /app

WORKDIR /app

COPY Gemfile Gemfile.lock ./

RUN gem install bundle

RUN bundle install

COPY . ./

EXPOSE 3000

CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]
