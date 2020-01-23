FROM ruby:2.6.4
WORKDIR /app

RUN apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get clean && \
    gem install bundler -v 1.17.2 && \
    rm -rf /var/lib/apt/lists/* /tmp/*

ADD Gemfile* /app/
RUN bundle check || bundle install --jobs=4 --retry=3

ADD . /app

ENTRYPOINT bundle exec puma -C config/puma.rb
