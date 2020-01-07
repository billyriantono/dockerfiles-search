FROM ruby:2.3-alpine
MAINTAINER Max Focker <max.focker.shih@gmail.com>

RUN gem install redis \
    && wget http://download.redis.io/redis-stable/src/redis-trib.rb
ENTRYPOINT ["ruby", "redis-trib.rb"]