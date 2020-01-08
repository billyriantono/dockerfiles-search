FROM ruby:2.5-slim
MAINTAINER exxk<exxk.lx@gmail.com>
RUN gem install redis
RUN mkdir /redis
WORKDIR /redis
ADD ./redis-trib.rb /redis/redis-trib.rb
