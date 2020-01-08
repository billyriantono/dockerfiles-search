FROM ruby:2.4.1-slim

RUN apt-get update -qq && apt-get install -y \
      build-essential \
      libpq-dev \
      nodejs \
      && rm -rf /var/lib/apt/lists/*

RUN gem update --system

ENV RAILS_VERSION 5.1.1

RUN gem install rails --version=$RAILS_VERSION

ENTRYPOINT ["rails"]
CMD ["--help"]

